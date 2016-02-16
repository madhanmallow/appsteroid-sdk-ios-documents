# FAQ

Last updated at 04/08/2014

---

|Question |Answer |
|---------|-------|
|What should I do if I find a problem with the SDK? |Please direct your inquiry to our support. |
|An SDK error keeps returning. What should I do? | Please refer to error code list. If this still does not resolve the issue, please contact us. |
|What iOS versions are supported? |iOS 6.0 and higher are supported. |
|How do I obtain an app identifier? |Please register on the Fresvii website. |
|Please tell me the steps for the initial setup. |Please refer to the SDK specifications. |
|I read the SDK specifications, but I still need help with the initial setup. |Please direct your inquiry to our support. |

---

### <a name="frequentquestions">Frequently Asked Questions</a>

#### <a name="apsanddatabase">- Where and How will the data be stored?</a>
Since AppSteroid is operated on AWS, all data created through the API calls will be managed on the AWS database.  We may cache data locally for non connected use of the AppSteroid platform, or to improve performance. Part of these persistence user data can be exported from the Web Console.


All AppSteroid user data is basically managed on the same database, and individual data can be distinguish by linking them to the application or the user. If you want the database to be private, we also offer a separate plan to support.


#### <a name="commonsystem">- If the system is going to co-exist with our database, how should it be done?</a>
All AppSteroid user data are ensured to be unique and also can be identified by the ID.  If users are managed on your system, you must have a solution to relate your own user data with the AppSteroid user data.  If you are using any other third party services, we recommend you to treat one of the user data as a master, and link the other user data to it.

The data used in each service should be held by each service.  If you want to link the data between each services, you can preform it by calling the API provided by the service from the app. We currently do not provide any interface to communicate directly between the servers.

#### <a name="loadtest">- How much load can it handle？</a>
All data related to feature provided by AppSteroid, such as recorded videos, text logs and more, can be stored unlimitedly.
It is basically same as any other WEB service for perfomance on API responses. The performance may drop when there are rush on access, however, we put our best effort to prevent it by enhancing the server at high loading.  Up to date, we never had a server down or big issue on performance drop. (September 23, 2015)