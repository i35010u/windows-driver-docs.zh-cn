---
title: 建立临时网络连接
description: 建立临时网络连接
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a20fe1e1c90f2e019cdf9c639da9f886205da446
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715248"
---
# <a name="establish-temporary-network-connectivity"></a>建立临时网络连接


电信应用程序无法启动长期连接。 但是，如果需要与特定网络进行临时连接，可以使用移动宽带 API，如下所示：

1.  创建 [**IMbnConnectionManager**](/windows/win32/api/mbnapi/nn-mbnapi-imbnconnectionmanager)的实例。

2.  注册到 [**IMbnConnectionEvents**](/windows/win32/api/mbnapi/nn-mbnapi-imbnconnectionevents) 连接点。

3.  创建 [**IMbnInterfaceManager**](/windows/win32/api/mbnapi/nn-mbnapi-imbninterfacemanager)的实例。

4.  通过将帐户设备 ID 传递到[**IMbnInterfaceManager：： GetInterface**](/windows/win32/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface)获取设备的[**IMbnInterface**](/windows/win32/api/mbnapi/nn-mbnapi-imbninterface)接口。  (有关详细信息，请参阅 [解锁设备](unlock-a-device.md)。 ) 

5.  通过调用 [**IMbnConnectionManager：： GetConnection**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionmanager-getconnection)获取设备的 IMbnConnection 接口。

6.  通过调用 [**IMbnConnection：： Connect**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnection-connect)建立连接。 *ConnectionMode*参数必须设置为**MBN \_ 连接 \_ 模式 \_ TMP \_ 配置文件**，并且*strProfile*参数必须是移动宽带配置文件说明。

使用 [**IMbnConnectionEvents：： OnConnectComplete**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionevents-onconnectcomplete) 方法返回连接尝试的结果。 若要在完成后断开连接，请调用 [**IMbnConnection：:D isconnect**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnection-disconnect) 方法。 使用 [**IMbnConnectionEvents：： OnDisconnectComplete**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionevents-ondisconnectcomplete)返回状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

