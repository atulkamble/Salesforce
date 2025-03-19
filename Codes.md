// Week 2: Apex Class with Variables and Control Flow
public class Week2ApexClass {
    public String greeting;
    
    public Week2ApexClass(String name) {
        this.greeting = 'Hello, ' + name + '!';
    }
    
    public String getGreeting() {
        return greeting;
    }
}

// Week 3: Apex Trigger to Update a Field when a Record is Inserted/Updated
trigger AccountTrigger on Account (before insert, before update) {
    for (Account acc : Trigger.new) {
        acc.Description = 'Updated via Trigger';
    }
}

// Week 4: SOQL Query and DML Operations
public class Week4SOQLDML {
    public static List<Account> getAccounts() {
        return [SELECT Id, Name FROM Account WHERE Industry = 'Technology'];
    }
    
    public static void updateAccount(String accId) {
        Account acc = [SELECT Id, Name FROM Account WHERE Id = :accId LIMIT 1];
        acc.Name = 'Updated Name';
        update acc;
    }
}

// Week 5: Apex Class with Methods
public class Week5ApexMethods {
    public static String getAccountName(String accId) {
        Account acc = [SELECT Name FROM Account WHERE Id = :accId LIMIT 1];
        return acc.Name;
    }
}

// Week 6: Apex Test Class
@isTest
private class Week6TestClass {
    @isTest
    static void testMethod() {
        Account acc = new Account(Name = 'Test Account');
        insert acc;
        Test.startTest();
        acc.Name = 'Updated Test Account';
        update acc;
        Test.stopTest();
        System.assertEquals('Updated Test Account', [SELECT Name FROM Account WHERE Id = :acc.Id].Name);
    }
}

// Week 7: Apex Callout to REST API
public class Week7RestCallout {
    @future(callout=true)
    public static void makeCallout() {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('https://api.example.com/data');
        req.setMethod('GET');
        Http http = new Http();
        HttpResponse res = http.send(req);
        System.debug('Response: ' + res.getBody());
    }
}

// Week 8: Final Project - Custom CRM Application
public class CRMApplication {
    public static void createCustomer(String name, String industry) {
        Account acc = new Account(Name = name, Industry = industry);
        insert acc;
    }
    
    public static List<Account> getCustomers() {
        return [SELECT Id, Name, Industry FROM Account];
    }
}
