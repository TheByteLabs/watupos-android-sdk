# WatuPos SDK
##About
Our Point of Sale (POS) SDK is a software development kit that allows developers to integrate POS functionality into their own applications. The SDK includes a variety of features and benefits that can help streamline and enhance the POS experience for businesses and customers alike.
Functionalities:
*Load configuration:  allows businesses to securely store and retrieve sensitive information, such as payment processing keys and credentials, within the SDK. This information is then used to process payments and access other features in the SDK
*Purchase: allows businesses to process payments for goods and services. Supports a wide range of payment types, such as debit cards and USSD
*Real-time updates: The balance enquiry functionality can retrieve the balance information in real-time, so customers always have the most up-to-date information.



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

  
  
  
