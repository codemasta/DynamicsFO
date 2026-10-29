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
        RunnableClass::GettingTime();
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

}
```