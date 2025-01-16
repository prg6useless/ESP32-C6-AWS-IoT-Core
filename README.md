# MQTT-AWS with ESP32-C6

This project demonstrates how to connect an ESP32-C6 microcontroller to AWS IoT Core using MQTT protocol.

## Prerequisites

- ESP32-C6 development board
- PlatformIO
- AWS account
- AWS IoT Core setup

## Setup Instructions

1. **Clone the repository:**
    ```sh
    https://github.com/prg6useless/ESP32-C6-AWS-IoT-Core.git
    cd ESP32-C6-AWS-IoT-Core
    ```

2. **Add the esp-aws-iot repository in the components folder:**
    - Create a folder named `components` in your root directory.
    - Add the esp-aws-iot repository in the components folder.
      - `components/esp-aws-iot`
      - repository link : https://github.com/espressif/esp-aws-iot.git 
      - (clone the release/v3.1.x branch)

3. **Configure AWS IoT Core and Add Certificates to the project:**
    - Create a new IoT Thing in AWS IoT Core.
    - Download the certificates and keys.
    - Attach a policy to the IoT Thing to allow MQTT operations.

    3.1 **Create and attach a policy:**
        - Create a new policy in AWS IoT Core with the following JSON:
          ```json
          {
            "Version": "2012-10-17",
            "Statement": [
              {
                "Effect": "Allow",
                "Action": [
                  "iot:Connect",
                  "iot:Receive",
                  "iot:Publish",
                  "iot:Subscribe"
                ],
                "Resource": "*"
              }
            ]
          }
          ```
        - Attach the policy to your IoT Thing.

    3.2 **Create the certs folder and rename the certificates:**
        - Create a folder named `certs` inside the src directory and add the AWS root certificate, private key and the device certificate.
        - rename the files as `aws-root-ca.pem`, `certificate.pem.crt`, `private.pem.key`.

4. **Update the code:**
    - Open the project in your IDE.
    - Update the WiFi credentials in the code:
      ```cpp
      const char* ssid = "your_SSID";
      const char* password = "your_PASSWORD";
      ```
    - Update the AWS IoT endpoint and certificates:
        - Open menuconfig in platformio, navigate to Component config/Amazon Web Services IoT Platform.
        - Set the AWS IoT Endpoint Hostname to your AWS Iot Endpoint.
        - Save the changes and close the menuconfig.
    
    - Open the aws_iot_config.h file and change the thing name to the thing name on your IoT Core.
      ```cpp
      #define AWS_IOT_MQTT_CLIENT_ID "your_thing_name"
      #define AWS_IOT_MY_THING_NAME "your_thing_name" 
      ```

5. **Upload the code:**
    - Connect your ESP32-C6 to your computer.
    - Upload the code using your IDE.

6. **Monitor the output:**
    - Open the serial monitor to view the connection status and MQTT messages.

6. **Setup for other espressif devices:**
    - You can also make changes to the platformio.ini file to upload to other devices like esp32, esp32-c3 etc.
    - Just change the env and the board lines in the platformio.ini file.
    ```ini
    [env:esp32]
    platform = espressif32
    board = esp32
    framework = espidf
    monitor_speed = 115200
    ```

## Usage

Once the ESP32-C6 is connected to AWS IoT Core, you can publish and subscribe to MQTT topics. Modify the code to handle specific topics and payloads as per your requirements.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## Contact

For any questions or support, please contact [sainju.saral433@gmail.com](mailto:sainju.saral433@gmail.com).
