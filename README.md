# SM808 and Arduino UNO Communication System

This project implements a communication system using the SM808 module and Arduino UNO, providing capabilities for SMS traffic management, IMEI modification, USSD commands, and data collection.

## System Architecture

### Server-Side Implementation (C#)
- Inetlab SMPP Server for SMS handling
- RabbitMQ integration for message queuing
- REST API endpoints for device management
- Real-time monitoring and analytics
- SIM block detection system
- Multi-country device management
- Pre-translation service for SMS content

### Client-Side (Arduino)
- SM808 module integration
- Local message queuing
- Device health monitoring
- SIM status checking
- Multi-language support

## Hardware Requirements

- SM808 Module
- Arduino UNO
- SIM Card
- Power Supply (5V)
- Connecting Wires

## Software Requirements

### Server Requirements
- .NET Core 6.0 or later
- Inetlab SMPP Server
- RabbitMQ Server
- Grafana
- SQL Server/PostgreSQL
- Translation API integration

### Client Requirements
- Arduino IDE
- Required Arduino libraries
- SM808 driver

## Capabilities

### 1. SMS Traffic Management
- Push SMS messages via SMPP
- Receive and process incoming SMS
- Bulk SMS handling
- SMS queue management using RabbitMQ
- SIM block detection and monitoring
- Device health checks
- Pre-translation of SMS content
- Multi-language support

### 2. IMEI Management
- IMEI modification capabilities
- IMEI verification
- IMEI backup and restore
- Multi-country IMEI tracking

### 3. USSD Commands
- Execute USSD commands
- Process USSD responses
- Automated USSD operations
- Country-specific USSD codes

### 4. Recharge System
- Balance checking
- Recharge code processing
- Automated recharge management
- Multi-currency support

### 5. Data Collection and Monitoring
- SMS usage tracking
- Voice plan monitoring
- Data usage analytics
- Dashboard integration with Grafana
- Real-time device status monitoring
- SIM block detection and alerts
- Device ID tracking across countries
- SIM card ID tracking and management

## Device and SIM Management

### Multi-Country Device Tracking
- Unique device ID assignment
- Country-specific configurations
- Device location tracking
- Cross-border usage monitoring

### SIM Card Management
- SIM card ID tracking
- SIM status monitoring
- Block detection and alerts
- Country-specific SIM profiles
- SIM replacement tracking

### Block Alert System
```csharp
// Example SIM block detection and alert
public class SIMBlockMonitor {
    public void CheckSIMStatus(string deviceId, string simId) {
        var status = GetSIMStatus(simId);
        if (status == SIMStatus.Blocked) {
            SendBlockAlert(deviceId, simId);
            LogBlockEvent(deviceId, simId);
        }
    }
}
```

## Pre-Translation Service

### SMS Content Translation
```csharp
// Example pre-translation service
public class TranslationService {
    public async Task<string> TranslateMessage(string message, string targetLanguage) {
        // Implement translation logic
        return await Translate(message, targetLanguage);
    }
}
```

### Supported Languages
- English
- Spanish
- French
- German
- [Add other supported languages]

## Setup Instructions

1. **Server Setup**
   ```csharp
   // Example SMPP server configuration
   var server = new SmppServer();
   server.Start("0.0.0.0", 2775);
   ```

2. **Hardware Connection**
   - Connect SM808 module to Arduino UNO using appropriate pins
   - Insert SIM card into SM808 module
   - Connect power supply

3. **Software Setup**
   - Install required Arduino libraries
   - Configure serial communication parameters
   - Set up initial parameters in the code
   - Install and configure RabbitMQ server
   - Set up Grafana instance
   - Configure translation service

4. **Configuration**
   - Set up APN settings
   - Configure SMS center number
   - Initialize IMEI settings
   - Set up USSD command templates
   - Configure RabbitMQ queues and exchanges
   - Set up Grafana dashboards
   - Configure SMPP server parameters
   - Set up device and SIM tracking
   - Configure block alert system

## Usage

### Server-Side Operations
1. **SMPP Server Configuration**
   ```csharp
   // Example SMPP server setup
   var server = new SmppServer();
   server.Start("0.0.0.0", 2775);
   server.ClientConnected += (sender, args) => {
       // Handle client connection
   };
   ```

2. **Message Processing with Translation**
   ```csharp
   // Example message processing with translation
   server.MessageReceived += async (sender, args) => {
       var message = args.Message;
       var translatedMessage = await translationService.TranslateMessage(
           message.Text, 
           GetTargetLanguage(message.DestinationAddress)
       );
       // Process translated message
   };
   ```

3. **SIM Block Monitoring**
   ```csharp
   // Example SIM block monitoring
   var monitor = new SIMBlockMonitor();
   monitor.CheckSIMStatus(deviceId, simId);
   ```

### Client-Side Operations
1. **SMS Operations**
   ```arduino
   // Example SMS send command
   sendSMS("+1234567890", "Hello World");
   ```

2. **USSD Commands**
   ```arduino
   // Example USSD command
   sendUSSD("*123#");
   ```

3. **IMEI Operations**
   ```arduino
   // Example IMEI change
   changeIMEI("123456789012345");
   ```

4. **Device Health Check**
   ```arduino
   // Example device health check
   checkDeviceHealth();
   ```

5. **SIM Block Detection**
   ```arduino
   // Example SIM block check
   checkSIMStatus();
   ```

### Queue Management
- SMS messages are queued in RabbitMQ
- Priority-based message processing
- Automatic retry mechanism
- Queue monitoring and alerts

### Monitoring Dashboard
- Real-time SMS traffic visualization
- Device health status indicators
- SIM block detection alerts
- Queue statistics and performance metrics
- Historical data analysis
- Multi-country device tracking
- SIM card status monitoring

## Troubleshooting

Common issues and solutions:
1. **SMPP Connection Issues**
   - Verify server IP and port
   - Check firewall settings
   - Validate credentials
   - Monitor connection logs

2. **No Network Connection**
   - Check SIM card insertion
   - Verify APN settings
   - Ensure proper power supply
   - Check for SIM block status

3. **SMS Sending Failures**
   - Check SMS center number
   - Verify signal strength
   - Ensure sufficient balance
   - Check RabbitMQ queue status
   - Verify SMPP server status

4. **USSD Command Issues**
   - Verify USSD code format
   - Check network compatibility
   - Ensure proper timing between commands

5. **Queue Management Issues**
   - Check RabbitMQ server status
   - Verify queue configurations
   - Monitor queue backlogs
   - Check consumer status

6. **Monitoring Issues**
   - Verify Grafana connection
   - Check data source configurations
   - Monitor alert thresholds
   - Verify device health checks

7. **Translation Issues**
   - Verify translation service connection
   - Check language support
   - Monitor translation quality
   - Validate character encoding

8. **SIM Block Issues**
   - Check block detection system
   - Verify alert configurations
   - Monitor block patterns
   - Validate SIM status updates

## Safety and Compliance

- Ensure compliance with local regulations
- Follow proper IMEI modification guidelines
- Maintain data privacy standards
- Regular system updates and maintenance
- Implement proper queue security measures
- Monitor for SIM block incidents
- Secure SMPP server configuration
- Follow data protection regulations
- Implement proper device tracking protocols

## Support

For technical support and queries:
- Documentation updates
- Bug reporting
- Feature requests
- Queue management assistance
- Dashboard configuration help
- SMPP server configuration support
- Translation service support
- SIM block detection assistance
