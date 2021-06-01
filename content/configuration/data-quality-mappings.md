---
uid: DataQualityMappings
---

# Data Quality Mappings

By default, when the PI Web API processes BACnet protocol data, it maps BACnet reliability enumeration values (the `BACnetReliability` object property) to OPC quality codes as shown in the following table.

| Enum Integer | BACnet Reliability Enumeration   | OPC Quality Code |
|--------------|----------------------------------|------------------|
| 0            | no-fault-detected                | GOOD             |
| 1            | no-sensor                        | BAD              |
| 2            | over-range                       | QUESTIONABLE     |
| 3            | under-range                      | QUESTIONABLE     |
| 4            | open-loop                        | BAD              |
| 5            | shorted-loop                     | BAD              |
| 6            | no-output                        | BAD              |
| 7            | unreliable-other                 | QUESTIONABLE     |
| 8            | process-error                    | BAD              |
| 9            | multi-state-fault                | BAD              |
| 10           | configuration-error              | BAD              |
| 11           | _Reserved for a future addendum_ | N/A              |
| 12           | communication-failure            | BAD              |
| 13           | member-fault                     | BAD              |
| 14           | monitored-object-fault           | BAD              |
| 15           | tripped                          | BAD              |

## PI Web API Data Quality Mapping Example

To customize the data quality mappings for the BACnet protocol, edit the following default XML and import it into the PI Web API using the [PI Web API Admin Utility](https://docs.osisoft.com/bundle/pi-web-api/page/configuration-with-pi-web-api-admin-utility.html).

```xml
<?xml version="1.0" encoding="utf-8"?> 
<AF xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="OSIsoft.AF.xsd" SchemaVersion="2.0"> 
  <AFEnumerationSet> 
    <Name>__BACnet</Name> 
    <Description>Source=QUALITYMAP, Name=BACnet, Type=INTEGER, Format=UINT32, IsNullable=false</Description> 
    <AFEnumerationValue> 
      <Name>no-fault-detected</Name> 
      <Value>0</Value> 
      <Description>Quality=GOOD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>no-sensor</Name> 
      <Value>1</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>over-range</Name> 
      <Value>2</Value> 
      <Description>Quality=QUESTIONABLE</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>under-range</Name> 
      <Value>3</Value> 
      <Description>Quality=QUESTIONABLE</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>open-loop</Name> 
      <Value>4</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>shorted-loop </Name> 
      <Value>5</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>no-output </Name> 
      <Value>6</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>unreliable-other</Name> 
      <Value>7</Value> 
      <Description>Quality=QUESTIONABLE</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>process-error</Name> 
      <Value>8</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>multi-state-fault</Name> 
      <Value>9</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>configuration-error</Name> 
      <Value>10</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>communication-failure</Name> 
      <Value>12</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>member-fault</Name> 
      <Value>13</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>monitored-object-fault</Name> 
      <Value>14</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
    <AFEnumerationValue> 
      <Name>tripped</Name> 
      <Value>15</Value> 
      <Description>Quality=BAD</Description> 
    </AFEnumerationValue> 
  </AFEnumerationSet> 
</AF>
```
