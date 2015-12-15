---
description: na
keywords: na
pagetitle: List Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a48551f4-e9e6-4277-99ff-99f64dfbc2e8
robots: noindex,nofollow
---
# List Map Operations - Usage and Examples
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para />
  </introduction>
  <section>
    <title>List <token>mapop</token>s</title>
    <content>
      <para>The following table lists the List Map Operations available in <token>af_integration_full</token>:</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>
                <token>mapop</token>
              </para>
            </TD>
            <TD>
              <para>Description</para>
            </TD>
            <TD>
              <para>Parameters</para>
            </TD>
            <TD>
              <para>Output</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Create List</para>
            </TD>
            <TD>
              <para>Creates and initializes a List that can: </para>
              <list class="bullet">
                <listItem>
                  <para>Hold intermediate data</para>
                </listItem>
                <listItem>
                  <para>Use List operations (like GroupBy)</para>
                </listItem>
                <listItem>
                  <para>Be used for complex structure transformations</para>
                </listItem>
                <listItem>
                  <para>Contain other container <token>mapop</token>s, including ForEach Loop and MapEach Loop.</para>
                </listItem>
              </list>
              <para>A List is like a table. A List has a set of <legacyBold>Members</legacyBold> (like columns in table) and a set of <legacyBold>Items</legacyBold> (like rows in a table). A List can be grouped.</para>
            </TD>
            <TD>
              <para>Member Name: Add the members of the List.</para>
              <para>Member Type: Click the type of the Member Name: String, Number, or Boolean.</para>
              <para>Use the <embeddedLabel>Add Item to List</embeddedLabel> <token>mapop</token> to add an item to the List.</para>
            </TD>
            <TD>
              <para>Every <token>mapop</token> within the Create List container should contribute on the path towards <legacyBold>Add Item to List</legacyBold>. <token>mapop</token>s that create target tree nodes (like MapEach and Conditional Assignment) are not allowed within the Create List scope container.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Add Item to List</para>
            </TD>
            <TD>
              <para>Adds an item to the list. Use <legacyItalic>only</legacyItalic> in the container of the Create List <token>mapop</token>.</para>
            </TD>
            <TD>
              <para>Can have at least 0 input parameters:</para>
              <table>
                <tbody>
                  <tr>
                    <TD>
                      <para>Input</para>
                    </TD>
                    <TD>
                      <para>A Member in a Create List or a link.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Condition</para>
                    </TD>
                    <TD>
                      <para>An expression to conditionally add items to the List. Can also be a link from a Logical Expression <token>mapop</token>.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </TD>
            <TD>
              <para>Results in an Item added to the <legacyBold>Add Item To List</legacyBold> <token>mapop</token>.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Select Unique Groups</para>
            </TD>
            <TD>
              <para>Generates groups from a list. Each group is identified by a unique value of the selected members. </para>
            </TD>
            <TD>
              <para>Requires <legacyItalic>exactly</legacyItalic> one input parameter:</para>
              <table>
                <tbody>
                  <tr>
                    <TD>
                      <para>Input</para>
                    </TD>
                    <TD>
                      <para>Required. A link to a Create List <token>mapop</token>. </para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Member</para>
                    </TD>
                    <TD>
                      <para>Required. Specify the Member to include in the output. If one Member is specified, the List is one Group for each unique Member value. If multiple Members are specified, the List-of-Groups will contain a Group for each unique combination of the Members value.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </TD>
            <TD>
              <para>A List containing a single Group or List-Of-Groups based on the Member value.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Select Value</para>
            </TD>
            <TD>
              <para>Selects the first item In a List. If a condition is specified, the first item in the list matching the condition is selected.</para>
            </TD>
            <TD>
              <para>Requires at least one parameter:</para>
              <table>
                <tbody>
                  <tr>
                    <TD>
                      <para>
                        <legacyItalic>Input</legacyItalic>
                      </para>
                    </TD>
                    <TD>
                      <para>Required. A link to a Create List <token>mapop</token>.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Select List Member: Select the member in the list to return.</para>
                    </TD>
                    <TD>
                      <para>Optional.  An expression to conditionally select items from the List.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Optional.  An expression to conditionally select items from the List.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </TD>
            <TD>
              <para>Accesses the value of the selected List Member and returns its value.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Select Entries</para>
            </TD>
            <TD>
              <para>Filters a List.</para>
            </TD>
            <TD>
              <para>Requires at least one parameter:</para>
              <table>
                <tbody>
                  <tr>
                    <TD>
                      <para>Input</para>
                    </TD>
                    <TD>
                      <para>Required.   A link to a Create List <token>mapop</token>. A constant or link can also be added.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Member</para>
                    </TD>
                    <TD>
                      <para>Optional. Specify the member to include in the output. If no members are specified, the output is not filtered by member.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Condition</para>
                    </TD>
                    <TD>
                      <para>Optional. An expression to conditionally filter items from the List.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
              <para />
            </TD>
            <TD>
              <para>Returns the filtered output.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Get Items</para>
            </TD>
            <TD>
              <para>Used in a ForEach or MapEach Loop. Gets the item in the list of the current iteration. When iterating over Unique Groups generated from a list, it returns the current group's items.</para>
            </TD>
            <TD>
              <para>No input parameters.</para>
            </TD>
            <TD>
              <para>Returns the current iteration.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Order By</para>
            </TD>
            <TD>
              <para>Orders items in a List. Key notes:</para>
              <list class="bullet">
                <listItem>
                  <para>Order By creates a new List. It does not modify the input List. The input List can still be used in other operations; these items are in a different order than the List returned by the Order By map operation.</para>
                </listItem>
                <listItem>
                  <para>Multiple members can be specified. In this scenario, Items in the List are sorted by the first specified Member. A tie between Items is resolved by comparing the second Member, and so on.</para>
                </listItem>
              </list>
              <para />
              <alert class="note">
                <para>Descending order is not supported.</para>
              </alert>
            </TD>
            <TD>
              <para>Requires exactly one input parameter:</para>
              <table>
                <tbody>
                  <tr>
                    <TD>
                      <para>
                        <legacyItalic>Input</legacyItalic>
                      </para>
                    </TD>
                    <TD>
                      <para>A link</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
              <para>After the link is created, choose the Member to sort. </para>
            </TD>
            <TD>
              <para>Returns a sorted list by the Member specified.</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>In the following examples, the All_Employees List contains four members: Emp_Id, Name, Designation, and Age. The All_Employees List has six Items:</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Emp_ID</para>
            </TD>
            <TD>
              <para>Name</para>
            </TD>
            <TD>
              <para>Designation</para>
            </TD>
            <TD>
              <para>Age</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>1</para>
            </TD>
            <TD>
              <para>A</para>
            </TD>
            <TD>
              <para>Developer</para>
            </TD>
            <TD>
              <para>25</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>2</para>
            </TD>
            <TD>
              <para>B</para>
            </TD>
            <TD>
              <para>Tester</para>
            </TD>
            <TD>
              <para>22</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>3</para>
            </TD>
            <TD>
              <para>C</para>
            </TD>
            <TD>
              <para>Developer</para>
            </TD>
            <TD>
              <para>26</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>4</para>
            </TD>
            <TD>
              <para>D</para>
            </TD>
            <TD>
              <para>Program Manager</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>5</para>
            </TD>
            <TD>
              <para>E</para>
            </TD>
            <TD>
              <para>Tester</para>
            </TD>
            <TD>
              <para>25</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>6</para>
            </TD>
            <TD>
              <para>F</para>
            </TD>
            <TD>
              <para>Manager</para>
            </TD>
            <TD>
              <para>36</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
    <sections>
      <section>
        <title>Select Unique Groups Example</title>
        <content>
          <para>Using the Age Member:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Age</para>
                </TD>
                <TD>
                  <para>
                    <legacyBold>Group 1 (Age = 25)</legacyBold>
                  </para>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>1</para>
                        </TD>
                        <TD>
                          <para>A</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>5</para>
                        </TD>
                        <TD>
                          <para>E</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <para />
                  <para />
                  <para>
                    <legacyBold>Group 2 (Age = 22)</legacyBold>
                  </para>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>2</para>
                        </TD>
                        <TD>
                          <para>B</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>22</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <para />
                  <para />
                  <para>
                    <legacyBold>Group 3 (Age = 26)</legacyBold>
                  </para>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>3</para>
                        </TD>
                        <TD>
                          <para>C</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>26</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <para />
                  <para />
                  <para>
                    <legacyBold>Group 4 (Age = 32)</legacyBold>
                  </para>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>4</para>
                        </TD>
                        <TD>
                          <para>D</para>
                        </TD>
                        <TD>
                          <para>Program Manager</para>
                        </TD>
                        <TD>
                          <para>32</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <para />
                  <para />
                  <para>
                    <legacyBold>Group 5 (Age = 36)</legacyBold>
                  </para>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>6</para>
                        </TD>
                        <TD>
                          <para>F</para>
                        </TD>
                        <TD>
                          <para>Manager</para>
                        </TD>
                        <TD>
                          <para>36</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <para />
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Select Value Example</title>
        <content>
          <para>Using the Name Member and specifying a Condition:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Name</para>
                  <para>Condition: item.Age&gt;25</para>
                </TD>
                <TD>
                  <table>
                    <tbody>
                      <tr>
                        <TD>
                          <para>Name</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>C</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>Using the Designation Member:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Designation</para>
                </TD>
                <TD>
                  <table>
                    <tbody>
                      <tr>
                        <TD>
                          <para>Developer</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Select Entries Example</title>
        <content>
          <para>Using the Emp_ID, Name and Age Members and specifying a Condition:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Emp_ID</para>
                  <para>Member: Name</para>
                  <para>Member: Age</para>
                  <para>Condition: item.Age&gt;25</para>
                </TD>
                <TD>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>3</para>
                        </TD>
                        <TD>
                          <para>C</para>
                        </TD>
                        <TD>
                          <para>26</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>4</para>
                        </TD>
                        <TD>
                          <para>D</para>
                        </TD>
                        <TD>
                          <para>32</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>6</para>
                        </TD>
                        <TD>
                          <para>F</para>
                        </TD>
                        <TD>
                          <para>36</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Get Items Example</title>
        <content>
          <para>Consider this scenario.</para>
          <para>You connect the All_Employees List to a MapEach Loop. This results in six iterations of the MapEach’s body. To access each individual Item in the All_Employees List, use a <embeddedLabel>Get Items</embeddedLabel> <token>mapop</token>. In this scenario, <embeddedLabel>Get Items</embeddedLabel> returns a <legacyItalic><legacyBold>List containing a single Item</legacyBold></legacyItalic>. This single Item is the current iteration variable. You can then use a <embeddedLabel>Select Value</embeddedLabel> <token>mapop</token> (without a Condition) to select a specific Member of this Item.</para>
        </content>
      </section>
      <section>
        <title>Order By Example</title>
        <content>
          <para>Using the Age Member:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Age</para>
                </TD>
                <TD>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>2</para>
                        </TD>
                        <TD>
                          <para>E</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>22</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>1</para>
                        </TD>
                        <TD>
                          <para>A</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>5</para>
                        </TD>
                        <TD>
                          <para>B</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>3</para>
                        </TD>
                        <TD>
                          <para>C</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>26</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>4</para>
                        </TD>
                        <TD>
                          <para>D</para>
                        </TD>
                        <TD>
                          <para>Program Manager</para>
                        </TD>
                        <TD>
                          <para>32</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>6</para>
                        </TD>
                        <TD>
                          <para>F</para>
                        </TD>
                        <TD>
                          <para>Manager</para>
                        </TD>
                        <TD>
                          <para>36</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>Using the Designation and Age Members:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Parameter</para>
                </TD>
                <TD>
                  <para>Output List</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Member: Designation</para>
                  <para>Member: Age</para>
                </TD>
                <TD>
                  <table>
                    <thead>
                      <tr>
                        <TD>
                          <para>Emp_ID</para>
                        </TD>
                        <TD>
                          <para>Name</para>
                        </TD>
                        <TD>
                          <para>Designation</para>
                        </TD>
                        <TD>
                          <para>Age</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD>
                          <para>1</para>
                        </TD>
                        <TD>
                          <para>A</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>3</para>
                        </TD>
                        <TD>
                          <para>C</para>
                        </TD>
                        <TD>
                          <para>Developer</para>
                        </TD>
                        <TD>
                          <para>26</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>6</para>
                        </TD>
                        <TD>
                          <para>F</para>
                        </TD>
                        <TD>
                          <para>Manager</para>
                        </TD>
                        <TD>
                          <para>36</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>4</para>
                        </TD>
                        <TD>
                          <para>D</para>
                        </TD>
                        <TD>
                          <para>Program Manager</para>
                        </TD>
                        <TD>
                          <para>32</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>2</para>
                        </TD>
                        <TD>
                          <para>E</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>22</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD>
                          <para>5</para>
                        </TD>
                        <TD>
                          <para>B</para>
                        </TD>
                        <TD>
                          <para>Tester</para>
                        </TD>
                        <TD>
                          <para>25</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section DoNotNumber="false">
        <title>Scope Container</title>
        <content>
          <para>When Create List is added to the <token>transform</token> design area, a scope container is created. All <token>mapop</token>s added to the container execute in the scope of that Loop container.</para>
          <para>For details on working within the scope container, see <link xlink:href="4a57af82-cae8-412d-a066-fb6a766d0be1">Working within the Scope</link>.</para>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>Error and Data Handling</title>
    <content>
      <para>
        <token>af_integration</token> provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of the following <ui>List</ui> <token>mapop</token>s is configurable: </para>
      <list class="bullet">
        <listItem>
          <para>
            <ui>Add Item to List</ui>
          </para>
        </listItem>
        <listItem>
          <para>
            <ui>Select Value</ui>
          </para>
        </listItem>
        <listItem>
          <para>
            <ui>Select Entries</ui>
          </para>
        </listItem>
      </list>
      <para>Steps:</para>
      <list class="ordered">
        <listItem>
          <para>Open a <ui><token>msgflow_proj</token></ui> or the <embeddedLabel>BizTalk Service Artifacts</embeddedLabel> project in <token>vsprvs</token>.</para>
        </listItem>
        <listItem>
          <para>Double-click a <token>transform</token> (.trfm) to open the <token>transform</token> Designer.</para>
        </listItem>
        <listItem>
          <para>In the <token>transform</token> toolbar, select <ui>Settings</ui>.</para>
        </listItem>
      </list>
      <para>
        <legacyBold>
          <ui>Error Handling</ui> tab</legacyBold>
      </para>
      <para>In the <ui>Error Handling</ui> tab, the following <ui>List</ui> <token>mapop</token>s have two <ui>Behavior</ui> options:</para>
      <list class="bullet">
        <listItem>
          <para>
            <ui>Add Item to List</ui>:</para>
          <list class="bullet">
            <listItem>
              <para>
                <ui>Fail map</ui>: The entire <token>transform</token> is aborted. Since <token>transform</token>s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.</para>
            </listItem>
            <listItem>
              <para>
                <ui>Do not add item into the list</ui>: If the <token>mapop</token> fails, the item is not added to the list in the output.</para>
            </listItem>
          </list>
        </listItem>
        <listItem>
          <para>
            <ui>Select Value</ui>:</para>
          <list class="bullet">
            <listItem>
              <para>
                <ui>Fail map</ui>: The entire <token>transform</token> is aborted. Since <token>transform</token>s are executed within a pipeline, an error occurs within the pipeline and the error is then sent to the client that sent the message.</para>
            </listItem>
            <listItem>
              <para>
                <ui>Output Null/Zero/False based on type of output</ui>: If the <token>mapop</token> fails, Null/Zero/False is returned as the output based on type of output.</para>
            </listItem>
          </list>
        </listItem>
        <listItem>
          <para>
            <ui>Select Entries</ui>:</para>
          <list class="bullet">
            <listItem>
              <para>
                <ui>Fail map</ui>: The entire <token>transform</token> is aborted. Since <token>transform</token>s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.</para>
            </listItem>
            <listItem>
              <para>
                <ui>Output an empty list</ui>: If the <token>mapop</token> fails, an empty list is returned as the output.</para>
            </listItem>
          </list>
        </listItem>
      </list>
      <para>
        <legacyBold>
          <ui>Null/Empty Data Handling</ui> tab</legacyBold>
      </para>
      <para>In the <ui>Null/Empty Data Handling</ui> tab, there are three options:</para>
      <list class="bullet">
        <listItem>
          <para>
            <ui>Consider empty nodes in cumulative operations</ui>: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.</para>
          <para>EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When <ui>Consider empty nodes in iterations</ui> is not checked, the <token>mapop</token> returns a value of seven. When <ui>Consider empty nodes in iterations</ui> is checked, the <token>mapop</token> returns a value of 10.</para>
        </listItem>
        <listItem>
          <para>
            <ui>Consider empty nodes in iterations</ui>: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.</para>
          <para>EXAMPLE: there is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When <ui>Consider empty nodes in iterations</ui> is not checked, the <token>mapop</token> iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When <ui>Consider empty nodes in iterations</ui> is checked, the <token>mapop</token> iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.</para>
        </listItem>
        <listItem>
          <para>
            <ui>Target Node Generation</ui>: If empty nodes are configured to be considered, you choose to generate an empty node in the output or to not generate an empty node in the output. Specifically:</para>
          <list class="bullet">
            <listItem>
              <para>Do not generate empty nodes: Default option.</para>
            </listItem>
            <listItem>
              <para>Generate empty nodes</para>
            </listItem>
          </list>
          <para>EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. <ui>Consider empty nodes in cumulative operations</ui> or <ui>Consider empty nodes in iterations</ui> are not checked, the <token>mapop</token> iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When <ui>Consider empty nodes in iterations</ui> is checked, the <token>mapop</token> iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section>
    <title>Known Issue</title>
    <content>
      <para>The <ui>Add Item To list</ui> <token>mapop</token> returns an error if the <ui>Create List</ui> <token>mapop</token> is populated <legacyItalic>after</legacyItalic> assigning inputs to the <ui>Add Item To list</ui> operation. For example:</para>
      <list class="ordered">
        <listItem>
          <para>Add a <ui>Create List</ui> to the design area.</para>
        </listItem>
        <listItem>
          <para>Add an <ui>Add Item To list</ui>  inside the <ui>Create List</ui>.</para>
        </listItem>
        <listItem>
          <para>Add an input link to the <ui>Add Item To list</ui>.</para>
        </listItem>
        <listItem>
          <para>Add a member value in the <ui>Create List</ui>.</para>
        </listItem>
      </list>
      <para>In this scenario, the input link is added to <ui>Add Item To list</ui>. Then, a member value is added to <ui>Create List</ui>. When you do this, the <ui>Add Item To list</ui> operation displays error:</para>
      <para>
        <legacyBold>Add Item to List operation labeled <legacyItalic>&lt;Name&gt;</legacyItalic> should add 1 member(s).</legacyBold>
      </para>
      <para>To work around this behavior, delete the input link to the <ui>Add Item To list</ui> and then redraw the link.</para>
    </content>
  </section>
  <section DoNotNumber="false">
    <title>Additional <token>mapop</token>s</title>
    <content>
      <para>
        <link xlink:href="a6b1c171-1871-4ef4-923b-d109104ddf14">String Operations</link>
      </para>
      <para>
        <link xlink:href="42b6bb45-6c49-466a-aed6-88811f0e40a1">Loop Operations</link>
      </para>
      <para>
        <link xlink:href="567064b1-5b6d-4209-baf1-c730279f8d04">Expressions</link>
      </para>
      <para>
        <link xlink:href="20c93d81-5f15-4545-8f60-24fa5479870d">Cumulative Operations</link>
      </para>
      <para>
        <link xlink:href="d52e64e7-120b-4186-828e-4a35cfcd5131">Date / Time Operations</link>
      </para>
      <para>
        <link xlink:href="cd6caf80-5425-41c1-a426-41071e5dba79">Misc Operations</link>
      </para>
    </content>
  </section>
  <relatedTopics>
    <link xlink:href="e102686a-b1c5-467d-8f22-8fadec19189f">Create a Transform or Map</link>
  </relatedTopics>
</developerConceptualDocument>