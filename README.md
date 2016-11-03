<html>
<head>

<script type="text/javascript">
    window.addEventListener(
            "load",
            function(){
                processTextAreas();
            },
            false
    );
    function processTextAreas(){
        var div, ta = document.getElementsByTagName('textarea');
        // need to walk backwards because we are deleting nodes when done with them
        // and walking forward would screw up element indices
        for (var i = ta.length -1; i>=0;i--){
            console.log('--------------------------------');
            console.log(ta[i].innerHTML);
            div = document.createElement('div');
            ta[i].parentNode.insertBefore(div,ta[i]);
            div.innerHTML = '<pre>' + ta[i].innerHTML + '</pre>';
            ta[i].parentNode.removeChild(ta[i]);
        }
    }
</script>
</head>
<body>
<div class="container">
    <h3> General Settings </h3>

    <p> All fields are in alphanumeric format. </p>

    <table class="api">
        <tr>
            <td><strong>Field Name</strong></td>
	        <td>Required</td>
            <td><strong>Notes</strong></td>
        </tr>
        <tr>
            <td><strong>merchant-id</strong></td>
            <td>Response Field Only</td>
            <td>Unique number identifying merchant</td>
        </tr>
        <tr>
            <td><strong>terminal-name</strong></td>
		    <td>Optional</td>
            <td>Desired name for individual terminal</td>
        </tr>
        <tr>
            <td><strong>terminal-id</strong></td>
             <td>Response Field Only</td>
            <td>Unique number identifying individual terminal</td>
        </tr>
        <tr>
            <td><strong>time-zone</strong></td>
            <td>Optional</td>
            <td>Time zone for the terminal. (Note: the value must be one of the following (case sensitive)- 'US/Alaska','US/Arizona','US/Central','US/East-Indiana','US/Eastern','US/Hawaii','US/Indiana-Starke','US/Michigan','US/Mountain','US/Pacific', 'UTC'.</td>
        </tr>
        <tr>
            <td><strong>batch-time-utc</strong></td>
            <td>Optional</td>
            <td>Time in utc when your terminal will settle all open batches</td>
        </tr>
        <tr>
            <td><strong>enable-auto-close-batch</strong></td>
            <td>Optional</td>
            <td>If false, you must manually settle all batches. If true, you will still be able to manually batch, but the terminal will automatically settle at the batch time indicated</td>
        </tr>

    </table>


    <h3> Change Terminal Settings </h3>

    <p>Use url https://gateway-sb.clearent.net/rest/v2/settings/terminal. You can PUT application/xml or application/json to the service. Make sure you provide a valid api-key in the header.</p>

    <table class="api" class="api">
        <tr>
            <td>XML Request</td>
            <td>XML Response</td>
        <tr>
            <td>
    <textarea>
   	<terminal-settings>
        <terminal-name>Terminal 1</terminal-name>
        <time-zone>US/Arizona</time-zone>
        <batch-time-utc>15:00</batch-time-utc>
        <enable-auto-close-batch>true</enable-auto-close-batch>
    </terminal-settings>
    </textarea>
            </td>
            <td>
    <textarea>
   	<response>
        <code>200</code>
        <status>SUCCESS</status>
        <exchange-id>ID-clasbgw01-gss01-de30c7f1-6dd3-4ac5-9037-e67916cefa12</exchange-id>
        <links>
            <rel>self</rel>
            <href>https://gateway-sb.clearent.net/rest/v2/settings/terminal</href>
        </links>
        <links>
            <rel>avs</rel>
            <href>https://gateway-sb.clearent.net/rest/v2/settings/terminal/avs</href>
        </links>
        <links>
            <rel>csc</rel>
            <href>https://gateway-sb.clearent.net/rest/v2/settings/terminal/csc</href>
        </links>
        <links>
            <rel>hpp</rel>
            <href>https://gateway-sb.clearent.net/rest/v2/settings/terminal/hpp</href>
        </links>
        <payload type="terminal-settings">
            <terminal-settings>
                <merchant-id>111111111111</merchant-id>
                <terminal-name>Gateway Settings Test Account</terminal-name>
                <terminal-id>11111111</terminal-id>
                <time-zone>US/Arizona</time-zone>
                <batch-time-utc>15:00</batch-time-utc>
                <enable-auto-close-batch>true</enable-auto-close-batch>
            </terminal-settings>
        </payload>
    </response>

    </textarea>
            </td>
        </tr>
        <tr>
            <td>JSON Request</td>
            <td>JSON Response</td>
        <tr>
            <td>
    <textarea>
        { 
            "terminal-name": "Terminal 1",
            "time-zone": "US/Arizona",
            "batch-time-utc": "15:00",
            "enable-auto-close-batch": "true"
        }
    </textarea>
            </td>
            <td>
    <textarea>
	{
        "code": "200",
        "status": "SUCCESS",
        "exchange-id": "ID-CLADEVGSOPS02-gss01-d5465fba-aca7-4ead-875b-082b1f14dd5b",
        "links": [
            {
                "rel": "avs",
                "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs"
            },
            {
                "rel": "csc",
                "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc"
            },
            {
                "rel": "self",
                "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal"
            }
        ],
        "payload": {
            "terminal-settings": {
                "merchant-id": "111111111111",
                "terminal-name": "Terminal 1",
                "terminal-id": "11111111",
                "time-zone": "US/Arizona",
                "batch-time-utc": "15:00",
                "enable-auto-close-batch": true
            },
            "payloadType": "terminal-settings"
        }
    }
    </textarea>
            </td>
        </tr>
    </table>


    

</div>

<div class="container">
    <h3>AVS Settings</h3>

    <p> All fields are in alpha-numeric format</p>

    <table class="api">
        <tr>
            <td><strong>Field Name</strong></td>
	        <td>Required</td>
            <td><strong>Notes</strong></td>
        </tr>
        <tr>
            <td><strong>enabled</strong></td>
            <td>Optional</td>
            <td>When true, Clearent will void the transaction unless certain AVS responses are received, even when the transaction receives an approval from the cardholder’s issuing bank. When AVS is disabled, Clearent will not stop transactions that receive an approval from the cardholder’s issuing bank. Clearent will send the address information if it is provided, which may be used by the bank in making its approval decision.</td>
        </tr>
        <tr>
            <td><strong>name</strong></td>
            <td>Required</td>
            <td>Name of specific AVS response. (Note: Value must be one of the following - 'ADDRESS_AND_NINE_DIGIT_ZIP_MATCH', 'ADDRESS_AND_FIVE_DIGIT_ZIP_MATCH', 'WHOLE_ZIP_MATCH_NOT_ADDRESS', 'FIVE_DIGIT_ZIP_MATCH_ADDRESS_DOES_NOT', 'ADDRESS_MATCH_ZIP_DOES_NOT', 'ADDRESS_AND_ZIP_DO_NOT_MATCH', 'ADDRESS_INFORMATION_NOT_VERIFIED', 'ISSUER_DOES_NOT_SUPPORT_AVS', 'ADDRESS_INFO_IS_UNAVAILABLE', 'TRANSACTION_INELIGIBLE', 'SYSTEM_UNAVAILABLE_OR_TIMEOUT')</td>
        </tr>
        <tr>
            <td><strong>allowed</strong></td>
		    <td>Required</td>
            <td>If false, Clearent will stop all transactions with that AVS response. If true, transactions with that response will be allowed.</td>
        </tr>
        <tr>
            <td><strong>description</strong></td>
             <td>Response Field Only</td>
            <td>A brief description of the response</td>
        </tr>
        <tr>
            <td><strong>response-code</strong></td>
              <td>Response Field Only</td>
            <td>One character standard identifying code used by issuing banks and payment networks.</td>
        </tr>

    </table>


    <h3>Change AVS Settings</h3>

    <p>Use url https://gateway-sb.clearent.net/rest/v2/settings/terminal/avs. You can PUT application/xml or application/json to the service.  Make sure you include a valid api-key in the header. You may include only the response-filters you wish to change in the request body, as long as you have at least one.</p>

    <table class="api" class="api">
        <tr>
            <td>XML Request</td>
            <td>XML Response</td>
        <tr>
            <td>
    <textarea>
   	<avs-settings>
        <enabled>true</enabled>
    	<response-filters>
    		<response-filter>
    			<name>ADDRESS_AND_NINE_DIGIT_ZIP_MATCH</name>
    			<allowed>true</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ADDRESS_AND_FIVE_DIGIT_ZIP_MATCH</name>
    			<allowed>true</allowed>
    		</response-filter>
    		<response-filter>
    			<name>WHOLE_ZIP_MATCH_NOT_ADDRESS</name>
    			<allowed>true</allowed>
    		</response-filter>
    		<response-filter>
    			<name>FIVE_DIGIT_ZIP_MATCH_ADDRESS_DOES_NOT</name>
    			<allowed>true</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ADDRESS_MATCH_ZIP_DOES_NOT</name>
    			<allowed>false</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ADDRESS_AND_ZIP_DO_NOT_MATCH</name>
    			<allowed>false</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ADDRESS_INFORMATION_NOT_VERIFIED</name>
    			<allowed>false</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ISSUER_DOES_NOT_SUPPORT_AVS</name>
    			<allowed>false</allowed>
    		</response-filter>
    		<response-filter>
    			<name>ADDRESS_INFO_IS_UNAVAILABLE</name>
    			<allowed>true</allowed>
    		</response-filter>
    		<response-filter>
    			<name>TRANSACTION_INELIGIBLE</name>
    			<allowed>false</allowed>
    		</response-filter>
    		<response-filter>
    			<name>SYSTEM_UNAVAILABLE_OR_TIMEOUT</name>
    			<allowed>false</allowed>
    		</response-filter>
    	</response-filters>
    </avs-settings>
    </textarea>
            </td>
            <td>
    <textarea>
    <response>
        <code>200</code>
        <status>SUCCESS</status>
        <exchange-id>ID-CLADEVGSOPS02-gss01-726116a8-918f-44c2-abe5-7466fc5dd3ca</exchange-id>
        <links>
            <rel>terminal</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal</href>
        </links>
        <links>
            <rel>csc</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc</href>
        </links>
        <links>
            <rel>self</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs</href>
        </links>
        <payload type="avs-settings">
            <avs-settings>
                <enabled>false</enabled>
                <response-filters>
                    <response-filter>
                        <name>ADDRESS_AND_NINE_DIGIT_ZIP_MATCH</name>
                        <response-code>X</response-code>
                        <allowed>false</allowed>
                        <description>Match of address and 9-digit zip code</description>
                    </response-filter>
                    <response-filter>
                        <name>ADDRESS_AND_FIVE_DIGIT_ZIP_MATCH</name>
                        <response-code>Y</response-code>
                        <allowed>false</allowed>
                        <description>Match of address and 5-digit zip code</description>
                    </response-filter>
                    <response-filter>
                        <name>WHOLE_ZIP_MATCH_NOT_ADDRESS</name>
                        <response-code>W</response-code>
                        <allowed>false</allowed>
                        <description>Match of 9-digit zip code; address does not match</description>
                    </response-filter>
                    <response-filter>
                        <name>FIVE_DIGIT_ZIP_MATCH_ADDRESS_DOES_NOT</name>
                        <response-code>Z</response-code>
                        <allowed>false</allowed>
                        <description>Match of 5-digit zip code; address does not match</description>
                    </response-filter>
                    <response-filter>
                        <name>ADDRESS_MATCH_ZIP_DOES_NOT</name>
                        <response-code>A</response-code>
                        <allowed>false</allowed>
                        <description>Address: Address Matches ZIP Does Not Match</description>
                    </response-filter>
                    <response-filter>
                        <name>ADDRESS_AND_ZIP_DO_NOT_MATCH</name>
                        <response-code>N</response-code>
                        <allowed>false</allowed>
                        <description>No: Address and ZIP Do Not Match</description>
                    </response-filter>
                    <response-filter>
                        <name>ADDRESS_INFORMATION_NOT_VERIFIED</name>
                        <response-code>G</response-code>
                        <allowed>false</allowed>
                        <description>Address information not verified</description>
                    </response-filter>
                    <response-filter>
                        <name>ISSUER_DOES_NOT_SUPPORT_AVS</name>
                        <response-code>S</response-code>
                        <allowed>false</allowed>
                        <description>Service Not Supported: Issuer does not support address verification</description>
                    </response-filter>
                    <response-filter>
                        <name>ADDRESS_INFO_IS_UNAVAILABLE</name>
                        <response-code>U</response-code>
                        <allowed>false</allowed>
                        <description>Address information is unavailable</description>
                    </response-filter>
                    <response-filter>
                        <name>TRANSACTION_INELIGIBLE</name>
                        <response-code>E</response-code>
                        <allowed>false</allowed>
                        <description>Error: Transaction ineligible for address verification</description>
                    </response-filter>
                    <response-filter>
                        <name>SYSTEM_UNAVAILABLE_OR_TIMEOUT</name>
                        <response-code>R</response-code>
                        <allowed>false</allowed>
                        <description>Retry: System Unavailable or Timeout</description>
                    </response-filter>
                </response-filters>
            </avs-settings>
        </payload>
    </response>

    </textarea>
            </td>
        </tr>
        <tr>
            <td>JSON Request</td>
            <td>JSON Response</td>
        <tr>
            <td>
    <textarea>

{
  "enabled": true,
  "response-filters": {
    "response-filter": [
      {
        "name": "ADDRESS_AND_NINE_DIGIT_ZIP_MATCH",
        "allowed": true
      },
      {
        "name": "ADDRESS_AND_FIVE_DIGIT_ZIP_MATCH",
        "allowed": true
      },
      {
        "name": "WHOLE_ZIP_MATCH_NOT_ADDRESS",
        "allowed": true
      },
      {
        "name": "FIVE_DIGIT_ZIP_MATCH_ADDRESS_DOES_NOT",
        "allowed": true
      },
      {
        "name": "ADDRESS_MATCH_ZIP_DOES_NOT",
        "allowed": false
      },
      {
        "name": "ADDRESS_AND_ZIP_DO_NOT_MATCH",
        "allowed": false
      },
      {
        "name": "ADDRESS_INFORMATION_NOT_VERIFIED",
        "allowed": false
      },
      {
        "name": "ISSUER_DOES_NOT_SUPPORT_AVS",
        "allowed": false
      },
      {
        "name": "ADDRESS_INFO_IS_UNAVAILABLE",
        "allowed": true
      },
      {
        "name": "TRANSACTION_INELIGIBLE",
        "allowed": false
      },
      {
        "name": "SYSTEM_UNAVAILABLE_OR_TIMEOUT",
        "allowed": false
      }
    ]
  }
}

    </textarea>
            </td>
            <td>
    <textarea>

{
  "code": "200",
  "status": "SUCCESS",
  "exchange-id": "ID-CLADEVGSOPS02-gss01-9ec5fb31-66de-493e-9e4c-5bb5f98ecdae",
  "links": [
    {
      "rel": "terminal",
      "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal"
    },
    {
      "rel": "csc",
      "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc"
    },
    {
      "rel": "self",
      "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs"
    }
  ],
  "payload": {
    "avs-settings": {
      "enabled": true,
      "response-filters": {
        "response-filter": [
          {
            "name": "ADDRESS_AND_NINE_DIGIT_ZIP_MATCH",
            "allowed": true,
            "description": "Match of address and 9-digit zip code",
            "response-code": "X"
          },
          {
            "name": "ADDRESS_AND_FIVE_DIGIT_ZIP_MATCH",
            "allowed": true,
            "description": "Match of address and 5-digit zip code",
            "response-code": "Y"
          },
          {
            "name": "WHOLE_ZIP_MATCH_NOT_ADDRESS",
            "allowed": true,
            "description": "Match of 9-digit zip code; address does not match",
            "response-code": "W"
          },
          {
            "name": "FIVE_DIGIT_ZIP_MATCH_ADDRESS_DOES_NOT",
            "allowed": true,
            "description": "Match of 5-digit zip code; address does not match",
            "response-code": "Z"
          },
          {
            "name": "ADDRESS_MATCH_ZIP_DOES_NOT",
            "allowed": false,
            "description": "Address: Address Matches ZIP Does Not Match",
            "response-code": "A"
          },
          {
            "name": "ADDRESS_AND_ZIP_DO_NOT_MATCH",
            "allowed": false,
            "description": "No: Address and ZIP Do Not Match",
            "response-code": "N"
          },
          {
            "name": "ADDRESS_INFORMATION_NOT_VERIFIED",
            "allowed": false,
            "description": "Address information not verified",
            "response-code": "G"
          },
          {
            "name": "ISSUER_DOES_NOT_SUPPORT_AVS",
            "allowed": false,
            "description": "Service Not Supported: Issuer does not support address verification",
            "response-code": "S"
          },
          {
            "name": "ADDRESS_INFO_IS_UNAVAILABLE",
            "allowed": true,
            "description": "Address information is unavailable",
            "response-code": "U"
          },
          {
            "name": "TRANSACTION_INELIGIBLE",
            "allowed": false,
            "description": "Error: Transaction ineligible for address verification",
            "response-code": "E"
          },
          {
            "name": "SYSTEM_UNAVAILABLE_OR_TIMEOUT",
            "allowed": false,
            "description": "Retry: System Unavailable or Timeout",
            "response-code": "R"
          }
        ]
      }
    },
    "payloadType": "avs-settings"
  }
}
    </textarea>
            </td>
        </tr>
    </table>
</div>

<div class="container">
<h3>CSC Settings</h3>

    <p> All fields are in alpha-numeric format</p>

    <table class="api">
        <tr>
            <td><strong>Field Name</strong></td>
	        <td>Required</td>
            <td><strong>Notes</strong></td>
        </tr>
        <tr>
            <td><strong>enabled</strong></td>
            <td>Optional</td>
            <td>When true, Clearent will void the transaction unless certain CSC responses are received, even when the transaction receives an approval from the cardholder’s issuing bank. When false, Clearent will not stop transactions that receive an approval from the cardholder’s issuing bank. Clearent will send the csc information if it is provided, which may be used by the bank in making its approval decision.</td>
        </tr>
        <tr>
            <td><strong>name</strong></td>
            <td>Required</td>
            <td>Name of specific CSC response. (Note: Value must be one of the following - 'CSC_MATCHED', 'CSC_NOT_MATCHED', 'NOT_PROCESSED', 'CSC_SHOULD_BE_ON_CARD_BUT_MERCHANT_SAID_IT_IS_NOT', 'UNKNOWN_OR_ISSUER_DID_NOT_PARTICIPATE', 'SERVICE_PROVIDER_DID_NOT_RESPONSE')</td>
        </tr>
        <tr>
            <td><strong>allowed</strong></td>
		    <td>Required</td>
            <td>If false, Clearent will stop all transactions with that CSC response. If true, transactions with that response will be allowed.</td>
        </tr>
        <tr>
            <td><strong>description</strong></td>
             <td>Response Field Only</td>
            <td>A brief description of the response</td>
        </tr>
        <tr>
            <td><strong>response-code</strong></td>
              <td>Response Field Only</td>
            <td>One character standard identifying code used by issuing banks and payment networks.</td>
        </tr>

    </table>


    <h3>Change CSC Settings</h3>

    <p>Use url https://gateway-sb.clearent.net/rest/v2/settings/terminal/csc. You can PUT application/xml or application/json to the service.  Make sure you include a valid api-key in the header. You may include only the response-filters you wish to change in the request body, as long as you have at least one.</p>

    <table class="api" class="api">
        <tr>
            <td>XML Request</td>
            <td>XML Response</td>
        <tr>
            <td>
    <textarea>
   	<avs-settings>
        <enabled>true</enabled>
    	<response-filters>
    		<response-filter>
                <name>CSC_MATCHED</name>
                <allowed>true</allowed>
            </response-filter>
            <response-filter>
                <name>CSC_NOT_MATCHED</name>
                <allowed>false</allowed>
            </response-filter>
            <response-filter>
                <name>NOT_PROCESSED</name>
                <allowed>true</allowed>
            </response-filter>
            <response-filter>
                <name>CSC_SHOULD_BE_ON_CARD_BUT_MERCHANT_SAID_IT_IS_NOT</name>
                <allowed>false</allowed>
            </response-filter>
            <response-filter>
                <name>UNKNOWN_OR_ISSUER_DID_NOT_PARTICIPATE</name>
                <allowed>true</allowed>
            </response-filter>
            <response-filter>
                <name>SERVICE_PROVIDER_DID_NOT_RESPONSE</name>
                <allowed>true</allowed>
            </response-filter>
    	</response-filters>
    </avs-settings>
    </textarea>
            </td>
            <td>
    <textarea>
    <response>
        <code>200</code>
        <status>SUCCESS</status>
        <exchange-id>ID-CLADEVGSOPS02-gss01-53a7ae96-c9ea-41fe-ab8d-21aab882e2ca</exchange-id>
        <links>
            <rel>terminal</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal</href>
        </links>
        <links>
            <rel>avs</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs</href>
        </links>
        <links>
            <rel>self</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc</href>
        </links>
        <payload type="csc-settings">
            <csc-settings>
                <enabled>true</enabled>
                <response-filters>
                    <response-filter>
                        <name>CSC_MATCHED</name>
                        <response-code>M</response-code>
                        <allowed>true</allowed>
                        <description>The CSC matches the issuing bank's records</description>
                    </response-filter>
                    <response-filter>
                        <name>CSC_NOT_MATCHED</name>
                        <response-code>N</response-code>
                        <allowed>false</allowed>
                        <description>The CSC does not match the issuing bank's records</description>
                    </response-filter>
                    <response-filter>
                        <name>NOT_PROCESSED</name>
                        <response-code>P</response-code>
                        <allowed>true</allowed>
                        <description>The CSC was not processed</description>
                    </response-filter>
                    <response-filter>
                        <name>CSC_SHOULD_BE_ON_CARD_BUT_MERCHANT_SAID_IT_IS_NOT</name>
                        <response-code>S</response-code>
                        <allowed>false</allowed>
                        <description>The card should have a CSC, but merchant indicated it was not present</description>
                    </response-filter>
                    <response-filter>
                        <name>UNKNOWN_OR_ISSUER_DID_NOT_PARTICIPATE</name>
                        <response-code>U</response-code>
                        <allowed>true</allowed>
                        <description>Card issuing bank does not participate</description>
                    </response-filter>
                    <response-filter>
                        <name>SERVICE_PROVIDER_DID_NOT_RESPONSE</name>
                        <response-code>X</response-code>
                        <allowed>true</allowed>
                        <description>Unknown / No response</description>
                    </response-filter>
                </response-filters>
            </csc-settings>
        </payload>
    </response>

    </textarea>
            </td>
        </tr>
        <tr>
            <td>JSON Request</td>
            <td>JSON Response</td>
        <tr>
            <td>
    <textarea>

    {
      "enabled": true,
      "response-filters": {
        "response-filter": [
          {
            "name": "CSC_MATCHED",
            "allowed": true
          },
          {
            "name": "CSC_NOT_MATCHED",
            "allowed": false
          },
          {
            "name": "NOT_PROCESSED",
            "allowed": true
          },
          {
            "name": "CSC_SHOULD_BE_ON_CARD_BUT_MERCHANT_SAID_IT_IS_NOT",
            "allowed": false
          },
          {
            "name": "UNKNOWN_OR_ISSUER_DID_NOT_PARTICIPATE",
            "allowed": true
          },
          {
            "name": "SERVICE_PROVIDER_DID_NOT_RESPONSE",
            "allowed": true
          }
        ]
      }
    }
    
        </textarea>
                </td>
                <td>
        <textarea>
    
    {
      "code": "200",
      "status": "SUCCESS",
      "exchange-id": "ID-CLADEVGSOPS02-gss01-f722a6db-9f60-4da7-b34c-494e01ca3bf1",
      "links": [
        {
          "rel": "terminal",
          "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal"
        },
        {
          "rel": "avs",
          "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs"
        },
        {
          "rel": "self",
          "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc"
        }
      ],
      "payload": {
        "csc-settings": {
          "enabled": true,
          "response-filters": {
            "response-filter": [
              {
                "name": "CSC_MATCHED",
                "allowed": true,
                "description": "The CSC matches the issuing bank's records",
                "response-code": "M"
              },
              {
                "name": "CSC_NOT_MATCHED",
                "allowed": false,
                "description": "The CSC does not match the issuing bank's records",
                "response-code": "N"
              },
              {
                "name": "NOT_PROCESSED",
                "allowed": true,
                "description": "The CSC was not processed",
                "response-code": "P"
              },
              {
                "name": "CSC_SHOULD_BE_ON_CARD_BUT_MERCHANT_SAID_IT_IS_NOT",
                "allowed": false,
                "description": "The card should have a CSC, but merchant indicated it was not present",
                "response-code": "S"
              },
              {
                "name": "UNKNOWN_OR_ISSUER_DID_NOT_PARTICIPATE",
                "allowed": true,
                "description": "Card issuing bank does not participate",
                "response-code": "U"
              },
              {
                "name": "SERVICE_PROVIDER_DID_NOT_RESPONSE",
                "allowed": true,
                "description": "Unknown / No response",
                "response-code": "X"
              }
            ]
          }
        },
        "payloadType": "csc-settings"
      }
    }
    </textarea>
            </td>
        </tr>
    </table>

</div>

<div class="container">
    <h3>HPP</h3>

    <p> All fields are in alpha-numeric format.</p>

    <table class="api">
        <tr>
            <td><strong>Field Name</strong></td>
	        <td>Required</td>
            <td><strong>Notes</strong></td>
        </tr>
        <tr>
            <td><strong>hpp-enabled</strong></td>
            <td>Optional</td>
            <td>If true, your terminal will have hpp capabilities. If false, it will not.</td>
        </tr>
        <tr>
            <td><strong>hpp-domain</strong></td>
		    <td>Optional</td>
            <td>This is the website URL where you will use the Hosted Payment Page</td>
        </tr>
        <tr>
            <td><strong>hpp-public-key</strong></td>
             <td>Response Field Only</td>
            <td>You need to use this Public Key so we can link your Hosted Payment Page to your account. Please do not publish this key outside of your code</td>
        </tr>

    </table>


    <h3>Change HPP settings</h3>

    <p>Use url https://gateway-sb.clearent.net/rest/v2/settings/terminal/csc. You can PUT application/xml or application/json to the service.  Make sure you include a valid api-key in the header.</p>

    <table class="api" class="api">
        <tr>
            <td>XML Request</td>
            <td>XML Response</td>
        <tr>
            <td>
    <textarea>
   	<hpp-settings>
        <hpp-enabled>true</hpp-enabled>
        <hpp-domain>https://example.com</hpp-domain>
    </hpp-settings>
    </textarea>
            </td>
            <td>
    <textarea>
   	<response>
        <code>200</code>
        <status>SUCCESS</status>
        <exchange-id>ID-CLADEVGSOPS02-gss01-2cf203be-a69d-449a-94bc-e36ba7b6693d</exchange-id>
        <links>
            <rel>terminal</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal</href>
        </links>
        <links>
            <rel>avs</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs</href>
        </links>
        <links>
            <rel>csc</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc</href>
        </links>
        <links>
            <rel>self</rel>
            <href>https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/hpp</href>
        </links>
        <payload type="hpp-settings">
            <hpp-settings>
                <hpp-public-key>307a301406072a8648ce3d020106092b240303020801010c036200047d9faeedfe9e82c5f532ca39d7bfdc053f151d60fd3316c8bbbf7d531760d2af0aae0c614047ab2ff495afbf9804b91b06fe9e57ae115ec785eacbded4e7cab26ee928f83c852cac5992c7e389bbfa7b2ddcae263ea808a39e7dc415fc9d7dad</hpp-public-key>
                <hpp-enabled>true</hpp-enabled>
                <hpp-domain>https://example.com</hpp-domain>
            </hpp-settings>
        </payload>
    </response>

    </textarea>
            </td>
        </tr>
        <tr>
            <td>JSON Request</td>
            <td>JSON Response</td>
        <tr>
            <td>
    <textarea>
    {
        "hpp-enabled": true,
        "hpp-domain": "https://example.com"
    }
    </textarea>
            </td>
            <td>
    <textarea>

    {
        "code": "200",
        "status": "SUCCESS",
        "exchange-id": "ID-CLADEVGSOPS02-gss01-1bc20e2c-cb4a-4211-96a8-ae5dd526feee",
        "links": [
            {
                "rel": "terminal",
                "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal"
            },
            {
              "rel": "avs",
              "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/avs"
            },
            {
              "rel": "csc",
              "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/csc"
            },
            {
              "rel": "self",
              "href": "https://cladevgsops02.clearent.net:8490/rest/v2/settings/terminal/hpp"
            }
        ],
        "payload": {
            "hpp-settings": {
                "hpp-public-key": "307a301406072a8648ce3d020106092b240303020801010c036200047d9faeedfe9e82c5f532ca39d7bfdc053f151d60fd3316c8bbbf7d531760d2af0aae0c614047ab2ff495afbf9804b91b06fe9e57ae115ec785eacbded4e7cab26ee928f83c852cac5992c7e389bbfa7b2ddcae263ea808a39e7dc415fc9d7dad",
                "hpp-enabled": true,
                "hpp-domain": "https://example.com"
            },
        "payloadType": "hpp-settings"
        }
    }
    </textarea>
            </td>
        </tr>
    </table>



</div>
</body>
</html>
