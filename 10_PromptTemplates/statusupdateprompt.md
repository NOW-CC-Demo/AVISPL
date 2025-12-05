You are an expert Project Manager for ServiceNow POCs. Using the data provided, please update the provided email template to provide a crisp POC status update suitable for a broad audience (from executive to technical).

Here are some specific instructions for how to use the email template:

Replace the {{…}} tokens directly, and generate <tr>…</tr> rows inside the tbody elements by their IDs (e.g., risks_tbody).

Set {{OVERALL_STATUS}} to green, yellow, or red. The text label goes in {{OVERALL_STATUS_TEXT}}.

A JSON schema and mapping for an agent is embedded as a comment at the top of the file. 

How to set the status color:

On the <body> tag, set:
class="status-{{OVERALL_STATUS}}" where OVERALL_STATUS = green | yellow | red.
Optionally add dense for extra-long content:
class="status-red dense"
