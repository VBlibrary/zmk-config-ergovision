 
Beginning of code writing for trackpads 
 

 trackpad0: trackpad0 {
        compatible = "cirque,trackpad";
        label = "Trackpad0";
        status = "disabled";

        /* Specify the I2C bus and address for the trackpad */
        i2c-bus = <&i2c0>;  // Correct I2C bus for Trackpad0
        i2c-address = <0x12>;  // Correct I2C address for Trackpad0
        gpio-sda = <&pro_micro 5 GPIO_ACTIVE_HIGH>; // GPIO pin for SDA for Trackpad0
        gpio-scl = <&pro_micro 6 GPIO_ACTIVE_HIGH>; // GPIO pin for SCL for Trackpad0
    };

    trackpad1: trackpad1 {
        compatible = "cirque,trackpad";
        label = "Trackpad1";
        status = "disabled";

        /* Specify the I2C bus and address for the trackpad */
        i2c-bus = <&i2c0>;  // Correct I2C bus for Trackpad1
        i2c-address = <0x13>;  // Correct I2C address for Trackpad1
        gpio-sda = <&pro_micro 5 GPIO_ACTIVE_HIGH>; // GPIO pin for SDA for Trackpad1
        gpio-scl = <&pro_micro 6 GPIO_ACTIVE_HIGH>; // GPIO pin for SCL for Trackpad1
    };