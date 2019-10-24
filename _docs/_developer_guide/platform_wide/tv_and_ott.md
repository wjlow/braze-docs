---
nav_title: TV and OTT Integrations
page_order: 4
---
# TV and OTT Integrations

As technology evolves to new platforms and devices, so can your messaging with Braze!

Braze offers different engagement channels for a number of different TV Operating Systems and "OTT" Set Top Boxes. 

## Platforms and Features

Below is a list of features and messaging channels supported today.

<style>
#tv-feature-table td {
    text-align: center !important;
    vertical-align: center;
}
</style>
<table id="tv-feature-table">
    <thead>
        <tr>
            <th>Device Type</th>
            <th>Data and Analytics</th>
            <th>Push Notifications</th>
            <th>In App Messages</th>
            <th>Canvas</th>
            <th>Content Cards</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Roku</td>
            <td for="data-analytics"><i class="fas fa-check text-success"></i></td>
            <td for="push"><i class="fas fa-times text-danger"></i></td>
            <td for="iam"><i class="fas fa-times text-danger"></i></td>
            <td for="canvas"><i class="fas fa-times text-danger"></i></td>
            <td for="content-cards"><i class="fas fa-times text-danger"></i></td>
        </tr>
        <tr>
            <td>Amazon Fire TV</td>
            <td for="data-analytics"><i class="fas fa-check text-success"></i></td>
            <td for="push"><i class="fas fa-check text-success"></i></td>
            <td for="iam"><i class="fas fa-check text-warning"></i><br>(via Data Model)</td>
            <td for="canvas"><i class="fas fa-check text-success"></i></td>
            <td for="content-cards"><i class="fas fa-check text-success"></i></td>
        </tr>
        <tr>
            <td>Kindle</td>
            <td for="data-analytics"><i class="fas fa-check text-success"></i></td>
            <td for="push"><i class="fas fa-check text-success"></i></td>
            <td for="iam"><i class="fas fa-check text-success"></i></td>
            <td for="canvas"><i class="fas fa-check text-success"></i></td>
            <td for="content-cards"><i class="fas fa-times text-danger"></i></td>
        </tr>
        <tr>
            <td>Android TV</td>
            <td for="data-analytics"><i class="fas fa-check text-success"></i></td>
            <td for="push"><i class="fas fa-check text-success"></i></td>
            <td for="iam"><i class="fas fa-check text-warning"></i><br>(via Data Model)</td>
            <td for="canvas"><i class="fas fa-check text-success"></i></td>
            <td for="content-cards"><i class="fas fa-check text-success"></i></td>
        </tr>
    </tbody>
</table>



### Roku

Use Braze's Roku SDK to collect data and analytics on your Roku users. These custom events and attributes can be used across your other channels for personalization and promotional messaging.

Coming soon is the ability to send In App Messages to your Roku users - stay tuned!

For more information, visit the [Roku Integration Guide]({{ site.baseurl }}/developer_guide/platform_integration_guides/roku/initial_sdk_setup/).

### Amazon Fire TV

Use Braze's Fire OS SDK to integrate with Amazon Fire TV devices. 

Features include:
* Data and Analytics collection for cross-channel engagement
* Push Notifications
* Content Cards
* In App Messages (custom handling is required)

For more information, visit the [Fire OS Integration Guide]({{ site.baseurl }}/developer_guide/platform_integration_guides/fireos/initial_sdk_setup/).

### Kindle

### Android TV