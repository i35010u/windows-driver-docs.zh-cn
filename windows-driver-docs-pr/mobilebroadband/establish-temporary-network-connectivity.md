---
title: 建立临时网络连接
description: 建立临时网络连接
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8ea34a9f97342dc900c71de00e8525d0ce80e78
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217317"
---
# <a name="establish-temporary-network-connectivity"></a>建立临时网络连接


电信应用程序无法启动长期连接。 但是，如果需要与特定网络进行临时连接，可以使用移动宽带 API，如下所示：

1.  创建 [**IMbnConnectionManager**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionmanager)的实例。

2.  注册到 [**IMbnConnectionEvents**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionevents) 连接点。

3.  创建 [**IMbnInterfaceManager**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)的实例。

4.  通过将帐户设备 ID 传递到[**IMbnInterfaceManager：： GetInterface**](/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface)获取设备的[**IMbnInterface**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)接口。  (有关详细信息，请参阅 [解锁设备](unlock-a-device.md)。 ) 

5.  通过调用 [**IMbnConnectionManager：： GetConnection**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionmanager-getconnection)获取设备的 IMbnConnection 接口。

6.  通过调用 [**IMbnConnection：： Connect**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-connect)建立连接。 *ConnectionMode*参数必须设置为**MBN \_ 连接 \_ 模式 \_ TMP \_ 配置文件**，并且*strProfile*参数必须是移动宽带配置文件说明。

使用 [**IMbnConnectionEvents：： OnConnectComplete**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-onconnectcomplete) 方法返回连接尝试的结果。 若要在完成后断开连接，请调用 [**IMbnConnection：:D isconnect**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-disconnect) 方法。 使用 [**IMbnConnectionEvents：： OnDisconnectComplete**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-ondisconnectcomplete)返回状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

