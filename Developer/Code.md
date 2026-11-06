```x++
internal final class RunnableClass
{
    /// <summary>
    /// Class entry point. The system will call this method when a designated menu 
    /// is selected or when execution starts and this class is set as the startup class.
    /// </summary>
    /// <param name = "_args">The specified arguments.</param>
    public static void main(Args _args)
    {
        // RunnableClass::GettingTime();
        RunnableClass::Insertion1();
    }

    public static void DeclareVariables()
    {
        int myInt;
        int64 myInt64;
        real myReal;
        str myStr;
        boolean myBool;
        date myDate;
        timeOfDay myTimeOfDay;
        container myContainer;
        guid myGuid;
        utcDateTime myUtcDateTime;

        // Print the default values of the variables
        info(strFmt("Default value of int: %1", myInt));
        info(strFmt("Default value of int64: %1", myInt64));
        info(strFmt("Default value of real: %1", myReal));
        info(strFmt("Default value of str: %1", myStr));
        info(strFmt("Default value of boolean: %1", myBool));
        info(strFmt("Default value of date: %1", myDate));
        info(strFmt("Default value of time: %1", time2Str(myTimeOfDay, TimeSeparator::Colon, TimeFormat::AMPM)));
        info(strFmt("Default value of container: %1", con2Str(myContainer)));
        info(strFmt("Default value of guid: %1", myGuid));
        info(strFmt("%1", myUtcDateTime));
    }

    public static void Enums()
    {
        
        PresenceStatus status;

        status = PresenceStatus::Available;

        info(strFmt("Presence status: %1", status));

        switch (status)
        {
            case PresenceStatus::Available:
                info("User is available.");
                break;
            case PresenceStatus::Busy:
                info("User is busy.");
                break;
     
            case PresenceStatus::Offline:
                info("User is offline.");
                break;
            default:
                info("Unknown presence status.");
                break;
        }
    }

    public static void Dialogs()
    {
        str name[2];
        Dialog dialog = new Dialog("Enter Information");

        DialogField firstName = dialog.addField(extendedTypeStr(String50));
        DialogField lastName = dialog.addField(extendedTypeStr(String50));

        firstName.label("Enter first name");
        lastName.label("Enter last name");

        if(dialog.run())
        {
            name[1] = firstName.value();
            name[2] = lastName.value();
            info(strFmt("First Name: %1 Last Name: %2", name[1], name[2]));
        }
        else
        {
            info("Dialog was canceled.");
        }
    }

    public static void Edts()
    {
        KokoEmployeeId EmployeeId;
        KokoEmployeeName employeeName;
        KokoGender employeeGender = KokoGender::Male;
    }

    public static void GettingTime()
    {
        utcdatetime currentTime;

        currentTime = DateTimeUtil::utcNow();

        info(strFmt("Current UTC Date and time: %1", currentTime));
    }

    public static void DataSelection1()
    {
        CustTable custTable;

        select firstonly custTable; //this is a short notation for select firstonly * from custTable
        info(strFmt("Customer account number: %1", custTable.AccountNum));
    }

    public static void DataSelection2()
    {
        CustTable custTable;

        while select firstonly10 custTable
        {
            info(strFmt("Customer account number: %1", custTable.AccountNum));
        }
    }

    public static void DataSelectionWithNext()
    {
        CustTable custTable;

        select custTable;
         
        info(strFmt("Customer account number: %1", custTable.AccountNum));

        next custTable;
        info(strFmt("Customer account number: %1", custTable.AccountNum));

        next custTable;
        info(strFmt("Customer account number: %1", custTable.AccountNum));

        next custTable;
        info(strFmt("Customer account number: %1", custTable.AccountNum));
    }

    public static void DataSelection3All()
    {
        CustTable custTable;
        select * from custTable;
        info(strFmt("Customer account number: %1", custTable.AccountNum));
    }

    public static void DataSelection3Specific()
    {
        CustTable custTable;
        select AccountNum, CustGroup from custTable;
        info(strFmt("Customer account number: %1, Customer group: %2", custTable.AccountNum, custTable.CustGroup));
    }

    public static void Insertion1()
    {
        KokoEmployeeTable employeeTable;

        ttsbegin;
        employeeTable.KokoEmployeeId                = 1;
        employeeTable.FirstName                     = "John";
        employeeTable.LastName                      = "Doe";
        employeeTable.EmployeeGender                = GenderMaleFemale::Male;
        employeeTable.Salary                        = 50000;
        employeeTable.KokoEmployeeDesignation       = "Software Engineer";
        employeeTable.insert();
        ttscommit;
    }

    public void Arrays()
    {
        int myArray[5]; // fixed-size array with 5 elements
        myArray[1] = 10;
        myArray[2] = 20;
        myArray[3] = 30;
        myArray[4] = 40;
        myArray[5] = 50;
        for (int i = 1; i <= 5; i++)
        {
            info(strFmt("Element %1: %2", i, myArray[i]));
        }

        // OR dimOf() function can be used to get the size of the array if the array is declared with a fixed size.
        for (int i = 1; i <= dimOf(myArray); i++)
        {
            info(strFmt("Element %1: %2", i, myArray[i]));
        }
    }

    public void Collections_Arrays()
    {
        Array myArray = new Array(Types::Integer);
        myArray.value(1, 10);
        myArray.value(2, 20);
        myArray.value(3, 30);

        //  accessing elements using the value() method
        info(strFmt("Element 1: %1", myArray.value(1)));

        for (int i = 1; i <= myArray.lastIndex(); i++)
        {
            info(strFmt("Element %1: %2", i, myArray.value(i)));
        }
    }

    public void Containers()
    {
        container myContainer = ["John", 30, true];
        str name = conPeek(myContainer, 1);
        int age = conPeek(myContainer, 2);
        boolean isActive = conPeek(myContainer, 3);
        info(strFmt("Name: %1, Age: %2, Active: %3", name, age, isActive));
    }

    public void ContainerOperations()
    {
        container myContainer = ["John", 30, true];
        info(strFmt("Container: %1", con2Str(myContainer)));

        // Adding an element to the container
        myContainer += "New Element";
        info(strFmt("Updated Container: %1", con2Str(myContainer)));

        // Removing an element from the container
        myContainer = conDel(myContainer, 2, 1); // Remove one element at position 2
        info(strFmt("After Removal: %1", con2Str(myContainer)));

        myContainer = conIns(myContainer, 2, "Inserted Element"); // Insert at position 2
        info(strFmt("After Insertion: %1", con2Str(myContainer)));

        myContainer = conPoke(myContainer, 1, "Updated Name"); // Update element at position 1
        info(strFmt("After Update: %1", con2Str(myContainer)));

        boolean isActive = conPeek(myContainer, 3); // Peek at position 3
        info(strFmt("Peeked Element: %1", isActive));

        str myStr;
        int myInt;
        [myStr, myInt] = myContainer; // Unpacking the container into variables
        info(strFmt("Unpacked Name: %1, Unpacked Age: %2", myStr, myInt));

        for (int i = 1; i <= conLen(myContainer); i++)
        {
            info(strFmt("Element %1: %2", i, conPeek(myContainer, i)));
        }
    }

}
```