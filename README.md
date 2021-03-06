# IBM-Project-Water-quality-IOT
	
[{"id":"eb9e0150.98164","type":"tab","label":"Flow 1","disabled":false,"info":""},
	{"id":"a965e02b.ddfe3","type":"ibmiot in","z":"eb9e0150.98164","authentication":"apiKey",
	"apiKey":"f157c0dc.e95ca","inputType":"evt","logicalInterface":"","ruleId":"","deviceId":"",
	"applicationId":"","deviceType":"+","eventType":"+","commandType":"","format":"json","name":"IBM IoT",
	"service":"registered","allDevices":true,"allApplications":"","allDeviceTypes":true,"allLogicalInterfaces":"",
	"allEvents":true,"allCommands":"","allFormats":true,"qos":0,"x":290.2897491455078,"y":148.8835220336914,"wires":[["3cf5fe23.5e7f92"]],"l":false},
	{"id":"c02477a5.0754a8","type":"debug","z":"eb9e0150.98164","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true",
	"targetType":"full","x":541.2840671539307,"y":149.96306228637695,"wires":[],"l":false},{"id":"3cf5fe23.5e7f92","type":"function","z":"eb9e0150.98164","name":"add params",
	"func":"   msg.payload.time = new Date().getTime();\n   msg.payload.deviceId = msg.deviceId;\n   return msg;","outputs":1,"noerr":0,"x":423.28979873657227,"y":148.00850868225098,
	"wires":[["c02477a5.0754a8","5e67918d.73db9"]],"l":false},{"id":"5e67918d.73db9","type":"cloudant out","z":"eb9e0150.98164","name":"","cloudant":"","database":"events",
	"service":"histdata1-ori-201910-cloudantNoSQLDB","payonly":true,"operation":"insert","x":539.2869338989258,"y":206.9005584716797,"wires":[],"l":false},{"id":"f157c0dc.e95ca",
	"type":"ibmiot","z":"","name":" IoT Platform","keepalive":"60","serverName":"x5mva4.messaging.internetofthings.ibmcloud.com","cleansession":true,"appId":"","shared":false}]
	

[{"id":"eb9e0150.98164","type":"tab","label":"Flow 1","disabled":false,"info":""},{"id":"a965e02b.ddfe3","type":"ibmiot in","z":"eb9e0150.98164","authentication":"apiKey",
	"apiKey":"f157c0dc.e95ca","inputType":"evt","logicalInterface":"","ruleId":"","deviceId":"","applicationId":"","deviceType":"+","eventType":"+","commandType":"","format":"json",
	"name":"IBM IoT","service":"registered","allDevices":true,"allApplications":"","allDeviceTypes":true,"allLogicalInterfaces":"","allEvents":true,"allCommands":"","allFormats":true,
	"qos":0,"x":95.28973817825317,"y":141.8835163116455,"wires":[["3cf5fe23.5e7f92"]],"l":false},{"id":"c02477a5.0754a8","type":"debug","z":"eb9e0150.98164","name":"","active":false,
	"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","x":332.2840623855591,"y":139.9630479812622,"wires":[],"l":false},{"id":"3cf5fe23.5e7f92",
	"type":"function","z":"eb9e0150.98164","name":"add params","func":"   msg.payload.time = new Date().getTime();\n   msg.payload.deviceId = msg.deviceId;\n   return msg;",
	"outputs":1,"noerr":0,"x":161.2897777557373,"y":141.00850820541382,"wires":[["c02477a5.0754a8","5e67918d.73db9","4eb3a306.a1925c"]],"l":false},
	{"id":"5e67918d.73db9","type":"cloudant out","z":"eb9e0150.98164","name":"","cloudant":"","database":"events","service":"histdata1-ori-201910-cloudantNoSQLDB",
	"payonly":true,"operation":"insert","x":329.28693675994873,"y":189.90055179595947,"wires":[],"l":false},{"id":"4eb3a306.a1925c","type":"function","z":"eb9e0150.98164",
	"name":"CtoF","func":"   msg.payload.tempF = msg.payload.temp*9/5+32;\n   return msg;","outputs":1,"noerr":0,"x":328.28974628448486,"y":248.83235359191895,
	"wires":[["221a66bf.3ecf6a"]],"l":false},{"id":"221a66bf.3ecf6a","type":"switch","z":"eb9e0150.98164","name":"tempAlerts","property":"payload.tempF","propertyType":"msg",
	"rules":[{"t":"gte","v":"190","vt":"num"},{"t":"gte","v":"175","vt":"num"},{"t":"gte","v":"150","vt":"num"},{"t":"else"}],"checkall":"false","repair":false,"outputs":4,
	"x":463.2869110107422,"y":246.82386016845703,"wires":[["b68dd141.9282"],["56b37fba.188c"],["e94fb1da.c081c"],["df9b1314.9f339"]],"l":false},
	{"id":"b68dd141.9282","type":"template","z":"eb9e0150.98164","name":"Extreme Temp","field":"payload.status","fieldType":"msg","format":"handlebars","syntax":"plain",
	"template":"Oxygen level low. Life threat to all aquatic organisms.","output":"str","x":552.2925844192505,"y":179.77270698547363,"wires":[["8a4543dc.ae1f6"]],"l":false},
	{"id":"e94fb1da.c081c","type":"template","z":"eb9e0150.98164","name":"Optimal Temp","field":"payload.status","fieldType":"msg","format":"handlebars","syntax":"plain",
	"template":"Perfect temperature for a healthy water body.","output":"str","x":555.0142307281494,"y":283.005654335022,"wires":[["8a4543dc.ae1f6"]],"l":false},
	{"id":"56b37fba.188c","type":"template","z":"eb9e0150.98164","name":"Low Temp","field":"payload.status","fieldType":"msg","format":"handlebars","syntax":"plain",
	"template":"Aquatic creatures will freeze to death.","output":"str","x":550.0142307281494,"y":233.00565433502197,"wires":[["8a4543dc.ae1f6"]],"l":false},
	{"id":"df9b1314.9f339","type":"switch","z":"eb9e0150.98164","name":"humidityAlert","property":"payload.humidity",
	"propertyType":"msg","rules":[{"t":"gte","v":"20","vt":"num"},{"t":"else"}],"checkall":"false","repair":false,"outputs":2,"x":528.2869110107422,"y":344.8210220336914,
	"wires":[["81c0afe9.04521"],["4cef2326.55395c"]],"l":false},{"id":"81c0afe9.04521","type":"template","z":"eb9e0150.98164","name":"Too humid","field":"payload.status",
	"fieldType":"msg","format":"handlebars","syntax":"plain","template":"Reduce humidity","output":"str","x":596.0142288208008,"y":325.0056743621826,"wires":[["8a4543dc.ae1f6"]],
	"l":false},{"id":"4cef2326.55395c","type":"template","z":"eb9e0150.98164","name":"Fine","field":"payload.status","fieldType":"msg","format":"handlebars","syntax":"plain",
	"template":"Everything's fine, no alert","output":"str","x":592.0142841339111,"y":377.005672454834,"wires":[["8a4543dc.ae1f6"]],
	"l":false},{"id":"8a4543dc.ae1f6","type":"rbe","z":"eb9e0150.98164","name":"Report be Exception","func":"rbe","gap":"","start":"","inout":"out","property":"payload.status",
	"x":652.2925872802734,"y":221.14203643798828,"wires":[["4fe54e44.4ec14"]],"l":false},{"id":"4fe54e44.4ec14","type":"debug","z":"eb9e0150.98164","name":"","active":true,
	"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.status","targetType":"msg","x":765.8351078033447,"y":220.96585273742676,"wires":[],"l":false},
	{"id":"f157c0dc.e95ca","type":"ibmiot","z":"","name":" IoT Platform","keepalive":"60","serverName":"x5mva4.messaging.internetofthings.ibmcloud.com",
	"cleansession":true,"appId":"","shared":false}]
	



 

