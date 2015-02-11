
For each visitor, IQNOMY uses a unique visitor id to track the pagevisits of a visitor on a tenants website.
To have more insight into who is visiting your website you can link an custom external id to the visitor.
There are 3 options available to do this.

=Option 1: a global Javascript variable=
To add an custom id to an IQNOMY visitor you can add a global Javascript variable _iqExternalVisitorId to your webpage. The Javascript variable will be processed by the IQNOMY script and the value will be linked to the visitor.
Make sure that the variable is initiated on the webpage before the IQNOMY is processed, otherwise the _iqExternalVisitorId will not be processed automatically.

 example:
 
 <script type="text/javascript">
      var _iqExternalVisitorId = "company_user_id_1"; </script>

=Option 2 HTML query string paramameter=
Alternatively you can add a HTML query string paramameter, _iqExternalVisitorId,to your webpage url. The value of the parameter will be linked to the visitor and can be used as the external visitor id.
Contact us if you want to use this method, so that we can enable this feature.

 example: www.mywebsite.com/home?_iqExternalVisitorId=company_user_id_1

=Option 3: using the IQImpressor Javascript object= 
You can also assign the external id manually. By using the IQImpressor Javascript object, available after the IQNOMY script is initiated, you can manually track an event. By calling
IQImpressor.trackEvent(tenantId,eventName,eventdata) you can trigger an event that will link a custom external id, to the visitor visiting your website.

 example:
 
 <script type="text/javascript">
 
       var tenantId = _iqsTenant
       var eventName = 'FORM'
       var eventdata = new Object();
           eventdata["_iqExternalVisitorId"] = "company_user_id_1";
 
       // You can only call this function after the IQNOMY has initialised.
       IQImpressor.trackEvent(tenantId,eventName,eventdata);
 
       var _iqExternalVisitorId = "company_user_id_1"; </script>


You can use both methods combined, but make sure that the given custom id is consistent, or external id of the visitor will change with the use of each method. Currently a IQNOMY user can only have one unique external id.

IQNOMY tracks visitors anonymously, so we advice not to use any privacy-sensitive custom id as an external id, like emailadresses.

=See also=
*[[Integration]]
