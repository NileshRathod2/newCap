public class accountControllerHandler {
     
    
     public static void updateFieldValues(List<Account> accList ,Map<Id , Account> oldMap){
         //
         Map<Id , Account> accToAccountMap = new Map<Id , Account>();
          List<Contact> lstContacts = new List<Contact>();
         for(Account acc:accList){
             if(oldMap != null && acc.BillingStreet != oldMap.get(acc.Id).BillingStreet ){
                 
                 accToAccountMap.put(acc.Id , acc);
             }
        }
         for(Contact con : [SELECT Id, MailingStreet  ,AccountId FROM Contact where AccountId IN: accToAccountMap.keySet()]){
             Contact c = new Contact();
             if(accToAccountMap.containsKey(con.AccountId)){
                 c.id= con.Id;
                 c.MailingStreet  = accToAccountMap.get(con.AccountId).BillingStreet;
                 lstContacts.add(c);
             }
         }
         if(!lstContacts.isEmpty()){
             update lstContacts;
         }
    }
    
    }
    //commit new changes on main as well as subBranch 
