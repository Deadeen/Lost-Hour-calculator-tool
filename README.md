# Contact Log Duration Calculator

This JavaScript function calculates the total duration of different types of contact logs (e.g., Ready, After Call Work, Outbound) from an XML string for a specific target date. It is designed to filter and process logs based on specific conditions, such as the `Topic` attribute and the `Uri` value.

## Function: `calculateTimes`

### Purpose
The `calculateTimes` function processes an XML string containing contact logs and calculates the total duration for the following categories:
- **Ready**: Logs with `Topic="Ready"`.
- **After Call Work (ACW)**: Logs with `Topic="After Call Work"`.
- **Outbound**: Logs with `Topic=""` (exactly an empty string) and a `Uri` starting with `+9`.

### Parameters
- `xmlContent` (String): The XML content as a string.
- `targetDate` (String): The target date in `YYYY-MM-DD` format. Only logs with a `CreateTime` starting with this date will be processed.

### Returns
An object with the following properties:
- `readyTime`: Total duration (in seconds) for logs with `Topic="Ready"`.
- `acwTime`: Total duration (in seconds) for logs with `Topic="After Call Work"`.
- `outboundTime`: Total duration (in seconds) for logs with `Topic=""` and `Uri` starting with `+9`.

### Example Usage
```javascript
const xmlContent = `
<ContactLogs>
    <ContactLog CreateTime="2023-10-01T10:00:00" Duration="120" Topic="Ready" />
    <ContactLog CreateTime="2023-10-01T10:05:00" Duration="60" Topic="After Call Work" />
    <ContactLog CreateTime="2023-10-01T10:10:00" Duration="180" Topic="">
        <ContactLogItem Uri="+91234567890" />
    </ContactLog>
</ContactLogs>
`;

const targetDate = "2023-10-01";
const result = calculateTimes(xmlContent, targetDate);

console.log(result);
// Output: { readyTime: 120, acwTime: 60, outboundTime: 180 }
