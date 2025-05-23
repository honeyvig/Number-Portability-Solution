# Number-Portability-Solution

🛠️ Open-Source Number Portability Solutions
1. YateNPDB (Yet Another Telephony Engine)

    Description: YateNPDB is a Number Portability Database designed to manage number portability information. It offers an API to set series or individually ported numbers.
    YateBTS

    Installation:

        Mageia OS:

uprmi.update -a;urpmi yate-npdb

CentOS:

yum makecache fast;yum install yate-npdb

Other Linux OSes:

        dnf makecache; dnf install yate-npdb

    Usage: After installation, you can add equipment of type npdb from the YateMMI web management interface. This allows you to manage ported numbers and series through the interface.
    YateBTS

2. NLKUP (Number Lookup)

    Description: NLKUP is a prototype of a number portability service for telecommunications operators. It implements an in-core data structure supporting lookup of phone numbers and retrieving their aliases.
    GitHub

    Features:

        Lookup: Retrieve alias for a given number.

        Insert: Enter a new alias for a given number.

        Delete: Remove a number's alias.

        Batch operations: Add/delete multiple numbers and their aliases.
        GitHub

    Access: The service is available via an HTTP-based protocol, providing endpoints for various operations.
    GitHub

📡 Number Portability APIs
1. Twilio Port In API

    Description: Twilio's Port In API allows you to check if a number can be ported to Twilio before starting the porting process. It also provides details about why a number cannot be ported or if manual actions are needed.
    Twilio+3Twilio+3Twilio+3

    Features:

        Check portability of a number.

        Retrieve reasons for non-portability.

        Manage port-in requests.
        developers.telnyx.com+11developers.telnyx.com+11Twilio+11
        zuelpay.com+10Twilio+10Twilio+10

    Documentation:
    Twilio

2. Telnyx Porting API

    Description: Telnyx offers a Porting API that allows you to verify the portability of a list of phone numbers. It provides detailed information about each number's portability status.
    Twilio+4developers.telnyx.com+4developers.telnyx.com+4

    Features:

        Verify portability of multiple numbers.

        Retrieve carrier information and coverage category.

        Identify reasons for non-portability.
        hlr-lookups.com+5MuleSoft Blog+5Nomios Group+5
        developers.telnyx.com

    Documentation:
    developers.telnyx.com

3. Agile Telecom MNP API

    Description: Agile Telecom provides a Mobile Number Portability (MNP) API that allows you to request mobile number portability information via an HTTP REST API.
    agiletelecom.com

    Features:

        Lookup number portability status.

        Retrieve operator and country information.

        Supports various authentication methods.
        GitHub
        agiletelecom.com
        developers.telnyx.com

    Documentation:
    agiletelecom.com

🐍 Python Script for Number Portability

Here's a Python script that utilizes the Telnyx Porting API to check the portability of a list of phone numbers:

import requests

# Replace with your Telnyx API key
API_KEY = 'your_telnyx_api_key'

# List of phone numbers to check
phone_numbers = [
    {'phone_number': '+13125354200'},
    {'phone_number': '+13125354500'}
]

# API endpoint
url = 'https://api.telnyx.com/origination/porting/portability_checks'

# Headers for authentication
headers = {
    'Authorization': f'Bearer {API_KEY}',
    'Content-Type': 'application/json'
}

# Payload
payload = {'phone_numbers': phone_numbers}

# Make the POST request
response = requests.post(url, json=payload, headers=headers)

# Check the response status
if response.status_code == 201:
    data = response.json()
    for item in data['phone_numbers']:
        print(f"Phone Number: {item['e164_number']}")
        print(f"Portable: {item['portable']}")
        print(f"Portability Status: {item['portability_status']}")
        print(f"Carrier: {item['carrier_name']}")
        print(f"Coverage Category: {item['coverage_category']}")
        print(f"Non-portable Reason: {item['non_portable_reason']}")
        print('-' * 40)
else:
    print(f"Failed to check portability: {response.status_code}")
    print(response.text)

📌 Notes:

    Replace 'your_telnyx_api_key' with your actual Telnyx API key.

    Ensure the phone numbers are in E.164 format (e.g., +13125354200).

    The script sends a POST request to the Telnyx API and prints the portability status for each number.
    developers.telnyx.com+1
