 
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

right overlay:

    &kscan0 {
	col-gpios
		= <&pro_micro 7  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 8  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 9  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 10 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 11 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 12 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		;
	sda-gpios = <&pro_micro 5 (GPIO_ACTIVE_HIGH | GPIO_PULL_UP)>;
	scl-gpios = <&pro_micro 6 (GPIO_ACTIVE_HIGH | GPIO_PULL_UP)>;
};


left overlay:

&kscan0 {
	col-gpios
		= <&pro_micro 7  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 8  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 9  (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 10 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 11 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		, <&pro_micro 12 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
		;
	
	sda-gpios = <&pro_micro 5 (GPIO_ACTIVE_HIGH | GPIO_PULL_UP)>;
	scl-gpios = <&pro_micro 6 (GPIO_ACTIVE_HIGH | GPIO_PULL_UP)>;
};


from 22.07.24
dtsi file deleted 
#include <dt-bindings/zmk/matrix_transform.h>

/ {
    chosen {
        zmk,kscan = &kscan0;
        zmk,matrix_transform = &default_transform;
    };

    default_transform: keymap_transform_0 {
        compatible = "zmk,matrix-transform";
        columns = <12>;
        rows = <5>;

        map = <
            RC(0,0) RC(0,1) RC(0,2) RC(0,3) RC(0,4) RC(0,5)                RC(0,6) RC(0,7) RC(0,8) RC(0,9) RC(0,10) RC(0,11)
            RC(1,0) RC(1,1) RC(1,2) RC(1,3) RC(1,4) RC(1,5)                RC(1,6) RC(1,7) RC(1,8) RC(1,9) RC(1,10) RC(1,11)
            RC(2,0) RC(2,1) RC(2,2) RC(2,3) RC(2,4) RC(2,5)                RC(2,6) RC(2,7) RC(2,8) RC(2,9) RC(2,10) RC(2,11)
            RC(3,0) RC(3,1) RC(3,2) RC(3,3) RC(3,4) RC(3,5)                RC(3,6) RC(3,7) RC(3,8) RC(3,9) RC(3,10) RC(3,11)                        
                                    RC(4,3) RC(4,4) RC(4,5)                RC(4,6) RC(4,7) RC(4,8)
        >;
    };

    kscan0: kscan {
        compatible = "zmk,kscan-gpio-matrix";
        wakeup-source;

        diode-direction = "col2row";
        row-gpios  
          = <&pro_micro 0 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
          , <&pro_micro 21 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
          , <&pro_micro 20 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
          , <&pro_micro 19 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
          , <&pro_micro 18 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>
          ;
    };
};

keymap rgo excluded for debugging
/*
 * Copyright (c) 2020 ZMK Contributors
 *
 * SPDX-License-Identifier: MIT
 */

#include <behaviors.dtsi>
#include <dt-bindings/zmk/keys.h>
#include <dt-bindings/zmk/bt.h>

/ {
    keymap {
        compatible = "zmk,keymap";

        default_layer {
            bindings = <
                &kp N6     &kp N7     &kp N8     &kp N9     &kp N0     &kp DELETE
                &kp Y      &kp U      &kp I      &kp O      &kp P      &kp RALT
                &kp H      &kp J      &kp K      &kp L      &kp SEMI   &kp RSHIFT
                &kp N      &kp M      &kp COMMA  &kp DOT    &kp SLASH  &kp RCTRL
            >;
        };
    };
};




temporary removed build.yaml
# This file generates the GitHub Actions matrix.
# For simple board + shield combinations, add them to the top level board and
# shield arrays, for more control, add individual board + shield combinations
# to the `include` property. You can also use the `cmake-args` property to
# pass flags to the build command and `artifact-name` to assign a name to
# distinguish build outputs from each other:
#
# board: [ "nice_nano_v2" ]
# shield: [ "corne_left", "corne_right" ]
# include:
#   - board: bdn9_rev2
#   - board: nice_nano_v2
#     shield: reviung41
#   - board: nice_nano_v2
#     shield: corne_left
#     cmake-args: -DCONFIG_ZMK_USB_LOGGING=y
#     artifact-name: corne_left_with_logging
#
---

include:
  #- board: nice_nano_v2
  #  shield: ergovision_left
 # - board: nice_nano_v2
 #   shield: ergovision_right
  - board: nice_nano_v2
    shield: settings_reset
  - board: nice_nano_v2
    shield: rgovision

    .github/yaml
    
    on: [push, pull_request, workflow_dispatch]

jobs:
  build:
    uses: zmkfirmware/zmk/.github/workflows/build-user-config.yml@main
