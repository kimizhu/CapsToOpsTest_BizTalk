---
description: na
keywords: na
pagetitle: Enable Encryption at Rest in BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72e428fd-250c-4d3a-b4ed-16c216094bbe
---
# Enable Encryption at Rest in BizTalk Services Portal
You can encrypt messages that are archived (also known as data at rest). This feature is called **Encryption at Rest** and can be enabled in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

## Enable encryption

1. Open the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

2. Select **Settings**.

3. Select the **Encryption At Rest** tab.

4. Select **Enable encryption for all messages being archived**. Enter the following properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |Key Name <br /> <br />|Enter the name of your encryption key. <br /> <br />|
   |Encryption Key <br /> <br />|Enter your encryption key. <br /> <br />|

5. **Save** your changes.

## What you need to know

- Messages are encrypted before being archived.

- The AES-256 encryption algorithm is used.

- If you change the existing encryption key, only new messages are encrypted with the new key. Older archived messages continue to remain encrypted with the previous key.

- When retrieving messages from the archive store, you need decrypt the messages using the key name and the encryption key.

- Messages being suspended in EDI receive/send are not automatically encrypted. The user can pass the messages through a pipeline and encrypt the message in that pipeline before routing it to [!INCLUDE[azure_2](/Token/azure_2_md.md)] storage.

## Create the encryption key
Using the following code, you can create an encryption key and the key name:

```c#
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApplication1
{
    class EncryptionAtRest
    {
        static void Main(string[] args)
        {
            // Enter this in B2B Portal UI for Encryption At Rest
            string userEncryptionKey = GetRandomBase64String(48);
            string userEncryptionKeyName = "userKey1";

            Stream encryptedArchiveStream = null;
            //Download encryptedArchiveStream from Blob

            Decrypt(encryptedArchiveStream, userEncryptionKey);
        }

        public static string GetRandomBase64String(int byteArraySize)
        {
            RNGCryptoServiceProvider RngProvider = new RNGCryptoServiceProvider();
            byte[] randomNumber = new byte[byteArraySize];
            RngProvider.GetBytes(randomNumber);
            string base64Text = Convert.ToBase64String(randomNumber);
            return base64Text;
        }

        public static Stream Decrypt(Stream encryptedStream, string userEncryptionKey)
        {
            byte[] byteEncryptionToken = Encoding.UTF8.GetBytes(userEncryptionKey);

            byte[] key = new byte[32];
            Array.Copy(byteEncryptionToken, key, 32);

            byte[] initializationVector = new byte[16];
            Array.Copy(byteEncryptionToken, 32, initializationVector, 0, 16);

            using (AesCryptoServiceProvider cryptoProvider = new AesCryptoServiceProvider())
            using (ICryptoTransform cryptoTransform = cryptoProvider.CreateDecryptor(key, initializationVector))
            {
                var memStream = new MemoryStream();
                CryptoStream encryptedCryptoStream = new CryptoStream(memStream, cryptoTransform, CryptoStreamMode.Write);
                encryptedStream.CopyTo(encryptedCryptoStream);
                encryptedCryptoStream.FlushFinalBlock();
                memStream.Seek(0, SeekOrigin.Begin);
                return memStream;
            }
        }
    }
}
```
