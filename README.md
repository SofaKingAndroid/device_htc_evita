<h1>HTC One XL Device Tree</h1>
<h3>Made for the Android Open Kang Project</h3>
------------------------------------------------

NOTE: The device trees are located in the other branches of this respository. Currently there are two other branches ("ics" = Android 4.0.x, "Ice Cream Sandwich" & "jb" = Android 4.1.x, "Jellybean")

Steps for building Jellybean:

1. Set up your system using AOSP's initializing source tutorial located here: http://source.android.com/source/initializing.html
2. Sync up with AOKP's source by making a new folder, changing directory to that folder, and running this command:

    <pre>repo init -u https://github.com/AOKP/platform_manifest.git -b jb
    repo sync</pre>

    It might take a long time depending on your connection speed. On my standard cable connection it takes 1 hour, approximately.

3. Create a file called "local_manifest.xml" under the ".repo" folder in the root of the source directory and add this into the file:

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <project path="kernel/htc/msm8960" name="htc-msm8960/android_kernel_htc_msm8960" remote="aokp" revision="android-msm-evita-3.0" />
            <project path="vendor/htc" name="htc-msm8960/proprietary_vendor_htc" remote="aokp" revision="jellybean" />
            <project path="device/htc/msm8960-common" name="htc-msm8960/android_device_htc_msm8960-common" remote="aokp" revision="jellybean" />
            <project path="device/htc/evita" name="rohanmathur/aokp_device_htc_evita" remote="aokp" revision="jb" />
        </manifest>

4. Re-sync the respositories by running:

    <pre>repo sync</pre>

5. Go to device/htc/evita and move the file "evita.mk" to vendor/aokp/products
6. Go to vendor/aokp/prodcts and add the following line to AndroidProducts.mk:

    <pre>$(LOCAL_DIR)/evita.mk \</pre>

7. Go to vendor/aokp/vendorsetup.sh and add the following line:

    <pre>add_lunch_combo aokp_evita-userdebug</pre>
    
8. That should be it for getting everything set up. Now to start building...
9. Run these commands, one after another:

    <pre>. build/envsetup.sh
    brunch evita</pre>
    
Thats it! You should have a flashable zip in a little bit! Be patient, building Android can take a very long time! It takes my 5 year old PC around 3 hours to build.