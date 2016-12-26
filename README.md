# Android8.1
package com.example.pankaj.preferences81;

import android.app.Activity;
import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.preference.PreferenceManager;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends Activity
{
    private static final int SETTINGS_RESULT = 1;
    Button settingButton;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        Button btnSettings=(Button)findViewById(R.id.buttonSettings);
        // start the UserSettingActivity when user clicks on Button
        btnSettings.setOnClickListener(new View.OnClickListener() {

            public void onClick(View v) {
                // TODO Auto-generated method stub
                Intent i = new Intent(getApplicationContext(), UserSettingActivity.class);
                startActivityForResult(i, SETTINGS_RESULT);
            }
        });
    }



    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data)
    {
        super.onActivityResult(requestCode, resultCode, data);

        if(requestCode==SETTINGS_RESULT)
        {
            displayUserSettings();
        }

    }


    private void displayUserSettings()
    {
        SharedPreferences sharedPrefs = PreferenceManager.getDefaultSharedPreferences(this);

        String  settings = "";

        settings=settings+"Password: " + sharedPrefs.getString("prefUserPassword", "NOPASSWORD");

        settings=settings+"\nRemind For Update:"+ sharedPrefs.getBoolean("prefLockScreen", false);

        settings=settings+"\nUpdate Frequency: "
                + sharedPrefs.getString("prefUpdateFrequency", "NOUPDATE");

        TextView textViewSetting = (TextView) findViewById(R.id.textViewSettings);

        textViewSetting.setText(settings);
    }

}
--------
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="updateFrequency">
        <item name="1">Daily</item>
        <item name="7">Weekly</item>
        <item name="3">Yearly</item>
        <item name="0">Never(I will Myself) </item>
    </string-array>
    <string-array name="updateFrequencyValues">
        <item name="1">1</item>
        <item name="7">7</item>
        <item name="30">30</item>
        <item name="0">0</item>
    </string-array>

</resources>
------
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android" >

    <PreferenceCategory android:title="Settings" >
        <EditTextPreference
            android:title="Password"
            android:summary="Set Your Password"
            android:key="prefUserPassword"/>
    </PreferenceCategory>

    <PreferenceCategory android:title="Security Settings" >
        <CheckBoxPreference
            android:defaultValue="false"
            android:key="prefLockScreen"
            android:summary="Lock The Screen With Password"
            android:title="Screen Lock" >
        </CheckBoxPreference>

        <ListPreference
            android:key="prefUpdateFrequency"
            android:title="Reminder for Updation"
            android:summary="Set Update Reminder Frequency"
            android:entries="@array/updateFrequency"
            android:entryValues="@array/updateFrequencyValues"
            />
    </PreferenceCategory>

</PreferenceScreen>
-------
package com.example.pankaj.preferences81;

import android.os.Bundle;
import android.preference.PreferenceActivity;

public class UserSettingActivity extends PreferenceActivity
{

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        // add the xml resource                     
        //addPreferencesFromResource(R.xml.user_settings);


    }

}
