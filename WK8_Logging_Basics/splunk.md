# A taste of Splunk 
## Step1. Download
Fill in the following details
![Alt text](./images/splunk_download.png?raw=true)

## Step2. Install
If there is a GUI, click install; otherwise, run
```
sudo dpkg -i splunk_xxx.deb
```

## Step3. Run splunk
At the first time running splunk, it will ask for the initial setup for the admin account.
![Alt text](./images/splunk_installation.png?raw=true)
```
cd /opt/splunk/bin/
sudo ./splunk start --accept-license
```

## Step4. Login to splunk
Use the username and password that you set in the last step to login

## Step5. Download the data
Let us download some sample data
https://data.montgomerycountymd.gov/
https://data.montgomerycountymd.gov/Finance-Tax-Property/County-Spending/vpf9-6irq

## Step6. Add the data to splunk
Add Data -> upload from my computer -> select *.csv from ~/Download

## Step7. A Few Selection

__Source type__: this helps Splunk to learn what data you have got. 
    * You specify a directory as a data source.
    * You specify a network input as a data source.
    * You specify a data source that has been forwarded from another Splunk instance.

Let us select "Automatic" in this short example.

__Host__: When the Splunk platform indexes data, each event receives a "host" value. The host value should be the name of the machine from which the event originates. The type of input you choose determines the available configuration options.

__Index__:The Splunk platform stores incoming data as events in the selected index. Consider using a "sandbox" index as a destination if you have problems determining a source type for your data. A sandbox index lets you troubleshoot your configuration without impacting production indexes. You can always change this setting later.

Let us use the default.

Now choose review

## Step9. You should see an error
The error is about Splunk cannot recognise the time format
go to `/opt/splunk/etc/system/local/props.conf`

add the following lines

```
TIMESTAMP_FIELDS = Invoice Date
TIME_FORMAT=%m/%d/%Y
```
and restart Splunk

```
cd /opt/splunk/bin/
./splunk restart
```

### Step10. Reload the data
Now there should be no error. Let us submit the data and start searching!

