<h1>HTC One XL Device Tree (AT&T HTC One X, evita)</h1>
<h3>Made for the Android Open Kang Project</h3>
------------------------------------------------

NOTE: The device trees are located in the other branches of this respository. Currently there are two other branches ("ics" = Android 4.0.x, "Ice Cream Sandwich" and "jb" = Android 4.1.x, "Jellybean"). I am using this "master" branch as a place for the readme :)

Steps for building Jellybean:

1. Set up your system using AOSP's initializing source tutorial located here: http://source.android.com/source/initializing.html
2. Sync up with AOKP's source by making a new folder, changing directory to that folder, and running this command:

    <pre>repo init -u https://github.com/AOKP/platform_manifest.git -b jb
    repo sync</pre>

    It might take a long time depending on your connection speed. On my standard cable connection it takes 1 hour, approximately.

3. Create a file called "local_manifest.xml" under the ".repo" folder in the root of the source directory and add this into the file:

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <project path="vendor/htc" name="rohanmathur/vendor_htc" remote="aokp" revision="jb" />
            <project path="device/htc/msm8960-common" name="htc-msm8960/android_device_htc_msm8960-common" remote="aokp" revision="jellybean" />
            <project path="device/htc/evita" name="rohanmathur/aokp_device_htc_evita" remote="aokp" revision="jb" />
        </manifest>

4. Re-sync the respositories by running:

    <pre>repo sync</pre>

5. Go to vendor/aokp/prodcts and add the following line to AndroidProducts.mk so that it is in alphabetical order by device codename:

    <pre>$(LOCAL_DIR)/evita.mk \</pre>

6. Make a file called "evita.mk" in the vendor/aokp/products folder and add the text below into it:

<pre># Specify phone tech before including full_phone
$(call inherit-product, vendor/aokp/configs/gsm.mk)

# Release name
PRODUCT_RELEASE_NAME := evita

TARGET_BOOTANIMATION_NAME := vertical-720x1280

# Inherit some common CM stuff.
$(call inherit-product, vendor/aokp/configs/common_phone.mk)

# Inherit device configuration
$(call inherit-product, device/htc/evita/device.mk)

# Device naming
PRODUCT_DEVICE := evita
PRODUCT_NAME := aokp_evita
PRODUCT_BRAND := htc
PRODUCT_MODEL := One X
PRODUCT_MANUFACTURER := HTC

# Set build fingerprint / ID / Product Name etc.
PRODUCT_BUILD_PROP_OVERRIDES += PRODUCT_NAME=htc_evita BUILD_FINGERPRINT=cingular_us/evita/evita:4.1.1/JRO03H/54373.1:user/test-keys PRIVATE_BUILD_DESC="1.85.502.1 CL54373 test-keys" BUILD_NUMBER=47741

PRODUCT_COPY_FILES += \
    vendor/aokp/prebuilt/bootanimation/bootanimation_720_1280.zip:system/media/bootanimation.zip </pre>

7. Go to vendor/aokp/vendorsetup.sh and add the following line, again so that it is in alphabetical order by device codename:

    <pre>add_lunch_combo aokp_evita-userdebug</pre>
    
8. Go to device/htc/evita and run this command:

    <pre>./setup-makefiles.sh</pre>
    
    Source should be downloaded and you should be all set to build now! Now onto building...
    
9. Run these commands, one after another from the root of the AOKP Source:

    <pre>. build/envsetup.sh
    brunch evita</pre>
    
Thats it! You should have a flashable zip in a little bit! Be patient, building Android can take a very long time! It takes my 5 year old PC around 3 hours to build.