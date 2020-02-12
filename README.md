# webusb-serial

Use with Zephyr webusb sample: https://github.com/zephyrproject-rtos/zephyr/tree/master/samples/subsys/usb/webusb

Can be accessed with address: https://xiongyihui.github.io/webusb-sample/

## For USB Composite Devices
To use WebUSB with a USB composite device on Windows 10, we need USB 2.1 and MS OS 2.0 Descriptor.

At the time of writing (2020-2-12), zephyr's default USB version is 2.0. We need to apply the following patch:

```
diff --git a/subsys/usb/usb_descriptor.c b/subsys/usb/usb_descriptor.c
index 6e25ba7fd4..eb9208ce1e 100644
--- a/subsys/usb/usb_descriptor.c
+++ b/subsys/usb/usb_descriptor.c
@@ -60,7 +60,7 @@ USBD_DEVICE_DESCR_DEFINE(primary) struct common_descriptor common_desc = {
        .device_descriptor = {
                .bLength = sizeof(struct usb_device_descriptor),
                .bDescriptorType = USB_DEVICE_DESC,
-               .bcdUSB = sys_cpu_to_le16(USB_2_0),
+               .bcdUSB = sys_cpu_to_le16(USB_2_1),
 #ifdef CONFIG_USB_COMPOSITE_DEVICE
                .bDeviceClass = MISC_CLASS,
                .bDeviceSubClass = 0x02,
```

Usage
=====

    $ python3 -m http.server
    Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
