---
title: findstack
description: Findstack 扩展查找所有包含指定的符号或模块的堆栈。
ms.assetid: 68a696f1-81fb-401e-ad68-ebc616eaf41a
keywords:
- findstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 453e6f5ab71044f9499551de6cc5672c29f61d11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541210"
---
# <a name="findstack"></a>！ findstack


**！ Findstack**扩展查找所有包含指定的符号或模块的堆栈。

```dbgcmd
!findstack Symbol [DisplayLevel]
!findstack -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *符号*   
指定符号或模块。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
指定显示应包含的内容。 这可以是以下值之一。 默认值为 1。

<span id="0"></span>**0**  
显示仅包含每个线程的线程 ID*符号*。

<span id="1"></span>**1**  
显示线程 ID 和包含每个线程的帧*符号*。

<span id="2"></span>**2**  
将显示包含每个线程的整个线程堆栈*符号*。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

堆栈跟踪的详细信息，请参阅[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

<a name="remarks"></a>备注
-------

[ **！ 堆栈**](-stacks.md)内核模式扩展还显示有关堆栈，包括每个线程的状态的简短摘要信息。

此扩展的输出的一些示例如下：

```dbgcmd
0:023> !uext.findstack wininet
Thread 009, 2 frame(s) match
        * 06 03eaffac 771d9263 wininet!ICAsyncThread::SelectThread+0x22a
        * 07 03eaffb4 7c80b50b wininet!ICAsyncThread::SelectThreadWrapper+0xd

Thread 011, 2 frame(s) match
        * 04 03f6ffb0 771cda1d wininet!AUTO_PROXY_DLLS::DoThreadProcessing+0xa1
        * 05 03f6ffb4 7c80b50b wininet!AutoProxyThreadFunc+0xb

Thread 020, 6 frame(s) match
        * 18 090dfde8 771db73a wininet!CheckForNoNetOverride+0x9c
        * 19 090dfe18 771c5e4d wininet!InternetAutodialIfNotLocalHost+0x220
        * 20 090dfe8c 771c5d6a wininet!ParseUrlForHttp_Fsm+0x135
        * 21 090dfe98 771bcb2c wininet!CFsm_ParseUrlForHttp::RunSM+0x2b
        * 22 090dfeb0 771d734a wininet!CFsm::Run+0x39
        * 23 090dfee0 77f6ad84 wininet!CFsm::RunWorkItem+0x79

Thread 023, 9 frame(s) match
        * 16 0bd4fe00 771bd256 wininet!ICSocket::Connect_Start+0x17e
        * 17 0bd4fe0c 771bcb2c wininet!CFsm_SocketConnect::RunSM+0x42
        * 18 0bd4fe24 771bcada wininet!CFsm::Run+0x39
        * 19 0bd4fe3c 771bd22b wininet!DoFsm+0x25
        * 20 0bd4fe4c 771bd706 wininet!ICSocket::Connect+0x32
        * 21 0bd4fe8c 771bd4cb wininet!HTTP_REQUEST_HANDLE_OBJECT::OpenConnection_Fsm+0x391
        * 22 0bd4fe98 771bcb2c wininet!CFsm_OpenConnection::RunSM+0x33
        * 23 0bd4feb0 771d734a wininet!CFsm::Run+0x39
        * 24 0bd4fee0 77f6ad84 wininet!CFsm::RunWorkItem+0x79

0:023> !uext.findstack wininet!CFsm::Run 0
Thread 020, 2 frame(s) match
Thread 023, 3 frame(s) match

0:023> !uext.findstack wininet!CFsm 0
Thread 020, 3 frame(s) match
Thread 023, 5 frame(s) match
```









