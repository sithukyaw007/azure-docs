---
title: APIs for Azure reservation automation | Microsoft Docs
description: Learn about the Azure APIs that you can use to programmatically get reservation information.
services: 'billing'
documentationcenter: ''
author: yashesvi
manager: yashesvi
editor: ''
tags: billing

ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/10/2018
ms.author: cwatson

---
# APIs for Azure reservation automation

Use Azure APIs to programmatically get information for your organization about Azure service or software reservations.

## Find reservation plans to buy

Use the Reservation recommendation API to get recommendations on which reservations plan to buy based on your organization's usage. For more information, see [Get reservation recommendations](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-recommendation).

You can also analyze your resource usage by using the Consumption API Usage Detail. For more information, see [Usage Details - List For Billing Period By Billing Account](/rest/api/consumption/usagedetails/listforbillingperiodbybillingaccount). The Azure resources that you use consistently are usually the best candidate for a reservation.

## Buy a reservation

You can't currently buy a reservation programmatically. To buy a reservation, see the following articles:

Service plans:
- [Virtual machine](../virtual-machines/windows/prepay-reserved-vm-instances.md?toc=/azure/billing/TOC.json)
-  [Cosmos DB](../cosmos-db/cosmos-db-reserved-capacity.md?toc=/azure/billing/TOC.json)
- [SQL Database](../sql-database/sql-database-reserved-capacity.md?toc=/azure/billing/TOC.json)

Software plans:
- [SUSE Linux software](../virtual-machines/linux/prepay-suse-software-charges.md?toc=/azure/billing/TOC.json)

## Get reservations

If you're an Azure customer with an Enterprise Agreement (EA customer), you can get the reservations your organization bought by using the [Get Reserved Instance transaction charges API](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-charges). For other subscriptions, get the list of reservations you bought and have permissions to view by using the API [Reservation Order - List](/rest/api/reserved-vm-instances/reservationorder/list). By default, the account owner or person that bought the reservation has permissions to view the reservation.

## See reservation usage

If you're an EA customer, you can programmatically view how the reservations in your organization are being used. For more information, see
[Get Reserved Instance usage for enterprise customers](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-usage). For other subscriptions, use the API [Reservations Summaries - List By Reservation Order And Reservation](/rest/api/consumption/reservationssummaries/listbyreservationorderandreservation).

If you find that your organization's reservations are being under-used:

- Make sure the virtual machines that your organization creates match the VM size that's on the reservation.
- Make sure instance size flexibility is on. For more information, see [Manage reservations - Change optimize setting for Reserved VM Instances](billing-manage-reserved-vm-instance.md#change-optimize-setting-for-reserved-vm-instances).
- Change the scope of reservation to shared so that it applies more broadly. For more information, see [Manage reservations - Change the scope for a reservation](billing-manage-reserved-vm-instance.md#change-the-scope-for-a-reservation).
- Exchange the unused quantity. For more information, see [Manage reservations - Cancellations and exchanges](billing-manage-reserved-vm-instance.md#cancellations-and-exchanges).

## Give access to reservations

Get the list of all reservations that a user has access to by using the [Reservation - Operation - List API](/rest/api/reserved-vm-instances/reservationorder/list). To give access to a reservation programmatically, see one of the following articles:

- [Manage access using RBAC and the REST API](../role-based-access-control/role-assignments-rest.md)
- [Manage access using RBAC and Azure PowerShell](../role-based-access-control/role-assignments-powershell.md)
- [Manage access using RBAC and Azure CLI](../role-based-access-control/role-assignments-cli.md)

## Split or merge reservation

After you buy more than one resource instance within a reservation, you may want to assign instances within that reservation to different subscriptions. You can change the reservation scope so that it applies to all subscriptions within the same billing context. But for cost management or budgeting purposes, you may want to keep the scope as "single subscription" and assign reservation instances to a specific subscription. 

To split a reservation, use the API [Reservation - Split](/rest/api/reserved-vm-instances/reservation/split). You can also split a reservation by using PowerShell. For more information, see [Manage reservations - Split reservation into two reservations](billing-manage-reserved-vm-instance.md#split-a-single-reservation-into-two-reservations).

To merge two reservations into one reservation, use the API [Reservation - Merge](/rest/api/reserved-vm-instances/reservation/merge).

## Change scope for a reservation

The scope of a reservation can be single subscription or all subscriptions in your billing context. If you set the scope to single subscription, the reservation is matched to running resources in the selected subscription. If you set the scope to shared, Azure matches the reservation to resources that run in all the subscriptions within the billing context. The billing context is dependent on the subscription you used to buy the reservation. For more information, see [Manage Reservations - Change the scope](billing-manage-reserved-vm-instance.md#change-the-scope-for-a-reservation).

To change the scope programmatically, use the API [Reservation - Update](/rest/api/reserved-vm-instances/reservation/update).

## Learn more

- [What are reservations for Azure](billing-save-compute-costs-reservations.md)
- [Understand how the VM reservation discount is applied](billing-understand-vm-reservation-charges.md)
- [Understand how the SUSE Linux Enterprise software plan discount is applied](billing-understand-suse-reservation-charges.md)
- [Understand how other reservation discounts are applied](billing-understand-reservation-charges.md)
- [Understand reservation usage for your Pay-As-You-Go subscription](billing-understand-reserved-instance-usage.md)
- [Understand reservation usage for your Enterprise enrollment](billing-understand-reserved-instance-usage-ea.md)
- [Windows software costs not included with reservations](billing-reserved-instance-windows-software-costs.md)
- [Azure Reservations in Partner Center Cloud Solution Provider (CSP) program](https://docs.microsoft.com/partner-center/azure-reservations)