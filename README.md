# Mati iOS SDK documentation 

![alt text](https://github.com/MatiFace/mati-global-id-sdk/blob/master/Group%2011-1.png)

## Xcode configurations

### POD File

Install Mati (your App pod file)
  
    pod 'Mati-Global-ID-SDK'
    
Update your pods from the terminal

    pod install

### Without POD File   

Download Mati framework from GitHub and add it to your project.

Note: Don't miss to add framework in Embedded Binaries.

### Xcode project build settings

In your XCode project Build Settings, please set

    "Enable Bitcode" to "No".

## AppDelegate - Mati KYC Initialisation

Make the following changes in your AppDelegate file 

### Swift
    
    import MatiGlobalIDSDK
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions
                     launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
          
          MFKYC.register(clientId:"{custom_token}")
    			//or
          MFKYC.register(clientId:"{custom_token}" identityId:"{identity_id}")
     	    
          return true
      }
      
      
      
### Objective-C
    
    #import <MatiGlobalIDSDK/MatiGlobalIDSDK.h>
    
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        
        [MFKYC registerWithClientId:@"{custom_token}"];
    		//or
        [MFKYC registerWithClientId:@"{custom_token}" identityId:@"{identity_id}"];

        return YES;
    }

## Mati KYC Button Placement (UI)

You now need to place the Mati KYC button inside your App. You have 2 options for that (interface builder vs. code):

You can include `MFKYCButton` into your view using XCode interface builder
Or
Add using Swift or Objective-C 

### Swift
    
    MFKYC.instance.metadata = ["key": "value"]
    let matiButton = MFKYCButton()
    matiButton.frame = CGRect(x: 0, y: 20, width: 320, height: 60)//you can change position, width and height
    matiButton.title = "Custom"
    view.addSubview(matiButton)
    
### Objective-C
    
    [MFKYC instance].metadata = @{"key": "value"};
    MFKYCButton *matiButton =[[MFKYCButton alloc] init];
    matiButton.frame = CGRectMake(0, 20, 320, 60);//you can change position,width and height
    matiButton.title = "Custom";
    [self.view addSubview:matiButton];
    
## Mati KYC Delegate

Use the delegate functions below in order to handle the success / failure of each verification.

### Swift

    //Assign the controller of your choice to be the Mati button delegate
    MFKYC.instance.delegate = self

    func mfKYCLoginSuccess(identityId: String) {
      print("Mati Login Success")
    }
    
    func mfKYCLoginCancelled() {
      print("Mati Login Failed")
    }
    
### Objective-C
    
    //Assign the controller of your choice to be the Mati button delegate
    [MFKYC instance].delegate = self;

    - (void)mfKYCLoginSuccessWithIdentityId:(NSString *)identityId {
        NSLog(@"Mati Login Success");
    }
    
    - (void)mfKYCLoginCancelled {
        NSLog(@"Mati Login Failed");
    }
