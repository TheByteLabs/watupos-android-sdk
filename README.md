# WatuPos SDK
## About
Our Point of Sale (POS) SDK is a software development kit that allows developers to integrate POS functionality into their own applications. The SDK includes a variety of features and benefits that can help streamline and enhance the POS experience for businesses and customers alike.
Functionalities:
* Load configuration:  allows businesses to securely store and retrieve sensitive information, such as payment processing keys and credentials, within the SDK. This information is then used to process payments and access other features in the SDK
* Purchase: allows businesses to process payments for goods and services. Supports a wide range of payment types, such as debit cards and USSD
* Real-time updates: The balance enquiry functionality can retrieve the balance information in real-time, so customers always have the most up-to-date information.



## Installation:
* Create a libs folder in your app directory and place the WatuPos SDK file (WatuPOS.aar) in it.
* Add the SDK as a dependency:
    * Navigate to File > Project Structure > Dependencies.
    * In the Declared Dependencies tab, click  and select Jar Dependency in the menu.
    * ![enter image description here](https://developer.android.com/static/studio/images/projects/psd-add-jar-dependency-dropdown.png)
    * In the Add Jar/Aar Dependency dialog, enter the path to the AAR file (libs/watupos.aar), then select the configuration to which the dependency applies. If the library should be available to all configurations, select the implementation configuration.
      ![enter image description here](https://developer.android.com/static/studio/images/projects/psd-add-aar-dependency.png)

Check your app’s build.gradle or build.gradle.kts file to confirm that a declaration similar to the following appears (depending on the build configuration you've selected):

    implementation files('libs/watupos.aar')

## Usage
Implement WatuPOS interface in your activity

    public class MainActivity extends AppCompatActivity implements WatuPOSInterface

Declare WatuPOS globally


    WatuPOS watuPOS;

Instantiate watuPOS (preferably in onCreate method) with your activity, terminal id, secret key and device type

      watuPOS = new WatuPOS(this,"YOUR-SECRET-KEY","TERMINAL-ID","DEVICE-TYPE");
Ensure your activity implements the onActivityResult callback method, and call watuPOS.process method in it

    @Override  
    protected void onActivityResult(int requestCode, int resultCode, Intent data)  
    {  
	    super.onActivityResult(requestCode, resultCode, data);   
	    watuPOS.process(data);   
    }  
Implement the watuCallback method. The json parameter in this callback method contains the final response of your method call.

    @Override  
    public void watuCallback(JSONObject response){  
	    Log.d("WaturResponse",response.toString());  
    }

Here is a sample of the response object

    {"code":200,"message":"Transaction Successful","data":{"isoResponseCode":"00","isoResponseMessage":"Approved"},"type":"read_card"}

## Methods

### Load POS Config

    watuPOS.loadKeys();

### Make Payment

    watuPOS.makePayment("AMOUNT","CASHBACK_AMOUNT", "TRANSACTION_TYPE", "RRN", "STAN");
### Print

    watuPOS.printText("TEXT_TO_PRINT");

## RESPONSE CODES

* 00 - Approved or completed successfully
* 01 - Refer to card issuer
02 - Refer to card issuer's special conditions
03 - Invalid merchant
04 - Pick-up
05 - Do not honor
06 - Error
07 - Pick-up card, special condition
08 - Honour with identification
09 - Request in progress
10 - Approved for partial amount
11 - Approved (VIP)
12 - Invalid transaction
13 - Invalid amount
14 - Invalid card number (no such number)
15 - No such issuer
16 - Approved, update track 3
17 - Customer cancellation
18 - Customer dispute
19 - Re-enter transaction
20 - Invalid response
21 - No action taken
22 - Suspected malfunction
23 - Unacceptable transaction fee
24 - File update not supported by receiver
25 - Unable to locate record on file
26 - Duplicate file update record, old record replaced
27 - File update field edit error
28 - File update file locked out
29 - File update not successful, contact acquirer
30 - Format error
31 - Bank not supported by switch
32 - Completed partially
33 - Expired card
34 - Suspected fraud
35 - Card acceptor contact acquirer
36 - Restricted card
37 - Card acceptor call acquirer security
38 - Allowable PIN tries exceeded
39 - No credit account
40 - Requested function not supported
41 - Lost card
42 - No universal account
43 - Stolen card, pick-up
44 - No investment account
51 - Not sufficient funds
52 - No checking account
53 - No savings account
54 - Expired card
55 - Incorrect personal identification number
56 - No card record
57 - Transaction not permitted to cardholder
58 - Transaction not permitted to terminal
59 - Suspected fraud
60 - Card acceptor contact acquirer
61 - Exceeds withdrawal amount limit
62 - Restricted card
63 - Security violation
64 - Original amount incorrect
65 - Exceeds withdrawal frequency limit
66 - Card acceptor call acquirer's security department
67 - Hard capture (requires that card be picked up at ATM)
68 - Response received too late
75 - Allowable number of PIN tries exceeded
90 - Cutoff is in process (switch ending a day's business and starting the next. Transaction can be sent again in a few minutes)
91 - Issuer or switch is inoperative
92 - Routing Error
93 - Transaction cannot be completed. Violation of law
94 - Duplicate transmission
95 - Reconcile error
96 - System malfunction
  
  
  
