---
title: SetupAPI 使用指南
description: SetupAPI 使用指南
ms.assetid: a5005a4e-206a-4971-b89d-0d8f833d38c8
keywords:
- 安装程序 Api 函数 WDK，准则
- 设备安装函数 WDK SetupAPI
- 常规安装函数 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6abc3b0fe5f41edd2dae26ee97c5d92bb843b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374563"
---
# <a name="guidelines-for-using-setupapi"></a>SetupAPI 使用指南





以下是使用的准则[常规安装函数](https://msdn.microsoft.com/library/windows/hardware/ff544985)(**安装 * **Xxx*) 和[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)(** SetupDi***Xxx*) 提供的安装程序 Api:

-   绝不能假定安装文件的内容是无错误，或者你提供的安装文件尚未被恶意修改了。 因此，始终验证从安装程序 Api 函数接收到的所有信息。 确认字符串是有效长度的缓冲区很大，有效大小的且索引值的有效范围内。

-   在编写 Microsoft Windows XP 和更高版本的系统上安装应用程序的安装，可以调用**SetupVerifyInfFile** （Windows SDK 文档中介绍），用于验证的数字签名的 INF 文件尚未修改。

-   始终测试每个安装程序 Api 函数的返回值。 如果函数失败，应调用你的代码[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)获取标识失败的错误代码。 返回的错误代码可以在中定义*Winerror.h*或*Setupapi.h*。 然后再调用**FormatMessage**借助 FORMAT_MESSAGE_FROM_SYSTEM 若要创建文本显示，始终使用 HRESULT_FROM_SETUPAPI 宏 (在中定义*Winerror.h*) 将返回值转换为HRESULT 值。 如果安装程序 Api 函数将返回成功，你的代码必须调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)。 ( [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)并**FormatMessage**函数，以及系统错误代码，Windows SDK 文档中所述。)

-   如果安装程序 Api 函数返回的句柄，您的代码必须检查返回值为 INVALID_HANDLE_VALUE。 此类函数不会返回**NULL**。

-   请注意以下不同之处 **SetupDi * * * Xxx*和 **安装 * * * Xxx*允许调用方的查询所需的缓冲区大小的函数：

    -   如果调用方的 **SetupDi * * * Xxx*函数创建此类查询[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)始终返回 ERROR_INSUFFICIENT_BUFFER。

    -   如果调用方的 **安装 * * * Xxx*函数创建此类查询[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)返回 NO_ERROR 如果没有缓冲区指定长度或 ERROR_INSUFFICIENT_BUFFER 缓冲区是否指定了太小。

 

 





