---
title: Configure Azure Load Balancer distribution mode
titleSuffix: Azure Load Balancer
description: In this article, get started configuring the distribution mode for Azure Load Balancer to support source IP affinity.
services: load-balancer
documentationcenter: na
author: asudbring
ms.service: load-balancer
ms.devlang: na
ms.topic: how-to
ms.custom: seodec18
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2021
ms.author: allensu
---

# Configure the distribution mode for Azure Load Balancer

Azure Load Balancer supports two distribution modes for distributing traffic to your applications:

* Hash-based
* Source IP affinity

In this article, you learn how to configure the distribution mode for your Azure Load Balancer.


## Configure distribution mode

---

# [**Azure portal**](#tab/azure-portal)

You can change the configuration of the distribution mode by modifying the load-balancing rule in the portal.

1. Sign in to the Azure portal and locate the resource group containing the load balancer you wish to change by clicking on **Resource Groups**.
2. In the load balancer overview screen, select **Load-balancing rules** under **Settings**.
3. In the load-balancing rules screen, select the load-balancing rule that you wish to change the distribution mode.
4. Under the rule, the distribution mode is changed by changing the **Session persistence** drop-down box. 

The following options are available: 

* **None (hash-based)** - Specifies that successive requests from the same client may be handled by any virtual machine.
* **Client IP (source IP affinity 2-tuple)** - Specifies that successive requests from the same client IP address will be handled by the same virtual machine.
* **Client IP and protocol (source IP affinity 3-tuple)** - Specifies that successive requests from the same client IP address and protocol combination will be handled by the same virtual machine.

5. Choose the distribution mode and then select **Save**.

:::image type="content" source="./media/load-balancer-distribution-mode/session-persistence.png" alt-text="Change session persistence on load balancer rule." border="true":::


# [**PowerShell**](#tab/azure-powershell)

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

Use PowerShell to change the load-balancer distribution settings on an existing load-balancing rule. The following command updates the distribution mode: 

```azurepowershell-interactive
$lb = Get-AzLoadBalancer -Name MyLoadBalancer -ResourceGroupName MyResourceGroupLB
$lb.LoadBalancingRules[0].LoadDistribution = 'sourceIp'
Set-AzLoadBalancer -LoadBalancer $lb
```

Set the value of the `LoadDistribution` element for the amount of load balancing required. 

Specify **sourceIP** for two-tuple (source IP and destination IP) load balancing. 

Specify **sourceIPProtocol** for three-tuple (source IP, destination IP, and protocol type) load balancing. 

Specify **default** for the default behavior of five-tuple load balancing.

---

## Next steps

* [Azure Load Balancer overview](load-balancer-overview.md)
* [Get started with configuring an internet-facing load balancer](quickstart-load-balancer-standard-public-powershell.md)
* [Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)