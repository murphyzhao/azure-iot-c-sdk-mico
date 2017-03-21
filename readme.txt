# readme.txt

azure_iot_c_sdk_mico SDK，基于 mico_A_v3.2.0 SDK
	请将本 SDK 所有文件，按照下边的目录结构放到 mico_A_v3.2.0 SDK 目录中
	注意：
		建议不要修改文件夹名称，一旦修改，需要对应更改mk文件的名称

Make Target命令：
	application.azure.azure_iothub_mqtt_demo@MK3165 total download run JTAG=stlink-v2
	注意：
		仿真器的设置，如果是jlink，默认不填写
		注意模块的选择

azure_iothub_mqtt_demo 说明：
	本 DEMO 移植于 azure-iot-sdk-c\iothub_client\samples\iothub_client_sample_mqtt\iothub_client_sample_mqtt.c
	azure-iot-sdk-c原始文件地址：
		https://github.com/Azure/azure-iot-sdk-c
	本 DEMO 使用 azure IOThub SDK 提供的 MQTT，支持QOS = 1，使用 TLS 加密

需要修改的地方：
	1、connectString、MESSAGE_COUNT、DOWORK_LOOP_NUM
		位置 azure_iothub_mqtt_demo\azure_config.h
	2、certificates (MQTT证书)
		位置 libraries/protocols/azure/certs/certs.c

PC端调试软件：
	Device Explorer Twin软件
	下载地址：		
		[Downloads\SetupDeviceExplorer.msi]https://github.com/Azure/azure-iot-sdks/releases

azure IOThub的基本操作流程：
	https://github.com/zhaojuntao/azure-iot-device-ecosystem/blob/master/get_started/MiCO-mxchipWiFiModule-c.md

目录结构：
	demos	
	│
	└─application
		│
		└─azure				
			│      
			└─azure_iothub_mqtt_demo
			        azure_config.h 				// azure 本地配置，结构体等相关定义
			        azure_iothub_mqtt_demo.mk 		
			        azure_main.c 				// azure 相关的处理函数
			        mico_app_define.h 			// azure-APP 相关信息的定义
			        mico_config.h 				// mico 相关的定义，无需修改
			        mico_main.c 				// application_start 函数入口
	libraries	
	│
	└─protocols
		│
		└─azure				
			│      
			├─azure_c_shared_utility 			//调用mico接口实现azure底层接口
			│      httpapi_mico.c
			│      platform_mico.c
			│      platform_mico.h
			│      tlsio_mico.c
			│      tlsio_mico.h
			│      azure_c_shared_utility.mk
			│      
			├─certs
			│      certs.c
			│      certs.h
			│      certs.mk
			│      
			├─iothub_client
			│      blob.c
			│      iothub_client.c
			│      iothub_client_ll.c
			│      iothub_message.c
			│      
			├─mico 								//开定时器，定时刷新NTP时间
			│      mico.mk
			│      mico_time.c
			│      mico_time.h
			│      
			├─parson
			│      parson.c
			│      parson.h
			│      parson.mk
			│      
			└─umqtt
			        mqtt_client.c
			        mqtt_codec.c
			        mqtt_message.c
			        umqtt.mk	        


UART 串口 log：
	[2][Platform: mico_platform_common.c:  98] Platform initialised, build by GNUC
	[675][BME280_USER: bme280_user.c: 480] BME280_ERROR: no i2c device found!
	[702][RTOS: mico_rtos_common.c:  84] Started MiCO RTOS interface for FreeRTOS v9.0.0
	[1141][SYSTEM: system_misc.c: 226] Free memory 199752 bytes
	[1151][SYSTEM: system_misc.c: 232] Kernel version: 32390002.050
	[1156][SYSTEM: system_misc.c: 235] MiCO version: 3.2.0
	[1161][SYSTEM: system_misc.c: 237] Wi-Fi driver version wl0: Jun 19 2016 22:40:05 version 7.45.45.17 (r64, mac 04:78:63:A0:01:1B
	[1173][SYSTEM: mico_system_init.c: 109] Available configuration. Starting Wi-Fi connection...
	[1181][SYSTEM: system_misc.c: 213] Connect to mxchip-offices.....
	[1189][SYSTEM: config_server.c: 147] Config Server established at port: 8000, fd: 1
	[5805][SYSTEM: system_misc.c:  75] Station up
	[5809][azure_mqtt_demo: mico_main.c:  50] wifi router was connected!
	[5815][azure_mqtt_demo: mico_main.c:  83] wifi connected successful
	[5818][azure_mqtt_demo: azure_main.c: 211]  azure_iothub_mqtt_demo firmware_version: ###
	[5821][azure_mqtt_demo: azure_main.c: 212] ****Memory info: total 226072, free 190184.
	[5829][azure_mqtt_demo: azure_main.c: 218] Start Azure IoT MQTT testing...
	[5836][azure_mqtt_demo: azure_main.c: 196] Azure IoT MQTT testing start.
	Info: IoT Hub SDK for C, version 1.1.2
	Info: IoTHubClient_LL_Create successfully
	[5851][azure_mqtt_demo: azure_main.c: 140] IoTHubClient_LL_SetMessageCallback...successful.
	...
	...
	...
	[52896][azure_mqtt_demo: azure_main.c: 188] Azure IoT MQTT testing has done.