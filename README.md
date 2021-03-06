### WiFi_Availability

**WiFi_Availability** is an Android application that scans the available Wi-Fi networks. To make it easier to see the Wi-Fi AP attributes, two seperate files are output that writes the attributes of Wi-Fi access points into a local file. In addition, it download and uploaded an 8 MByte file to an internet server to calculate the upload and download speeds. 
lets see some code examples.

### Create a directory and a file inside the directory
```java
    File folder = Environment.getExternalStoragePublicDirectory(DIRECTORY_DCIM);
    File Wi_Fi = new File(folder, "All_data.txt");
 ```     
 ### Give permission to access location and storage
 ```java
 int PERMISSION_ALL = 1;
                    String[] PERMISSIONS = {Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.ACCESS_FINE_LOCATION, Manifest.permission.ACCESS_COARSE_LOCATION};

                    if (!hasPermissions(activity, PERMISSIONS)) {
                        ActivityCompat.requestPermissions(activity, PERMISSIONS, PERMISSION_ALL);
                    }
```

### Scanning for WiFi Networks
You can perform a WiFi Network scan like so:
```java
List<ScanResult> availableNetworks = new ArrayList<ScanResult>();
                 availableNetworks = activity.wm.getScanResults();
```  
### Provide the upload and download links
```java
String SERVER_URL = "http://";
String urldownload = "http://";
```  

### Writing into a file function
```java
private void printInfo(File file, String Info, String trial) {
        BufferedWriter fos = null;
        try {
            fos = new BufferedWriter(new FileWriter(file, true));
            fos.write(Info);
            fos.flush();
            fos.close();
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
```    
    
### Output


There are three main files: 

1/ All_data : contains the raw data from the ScanResult Android

2/ Individual_AP_Tributes : contains refined data : 

Data,longitude,latitude,BSSID,RSSI,BSSID(first 10 characteristics),SSID,capabilities,frequency,timestamp,isPasspointNetwork,channelWidth,centerFreq0,centerFreq1, is80211mcResponder

3/ Extra_Information : contains information about the available networks:

Data,longitude,latitude,Number of total Wi-Fi networks,Number of open networks,max RSSI level,average RSSI level,min RSSU level,connected RSSI level,frequency,bandwidth,Mode,utilization,BSSID,SSID,download speed,upload speed
