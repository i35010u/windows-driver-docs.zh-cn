---
title: 带批注的 x86 反汇编
description: 带批注的 x86 反汇编
ms.assetid: ea1e67c8-d752-42d8-92db-a0c105ceddd6
keywords:
- x86 处理器，带批注的反汇编
- x86 处理器，程序集代码
- x86 处理器，源代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ffc922683f13ddbb2c4de0523439e3b9cb8a95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346349"
---
# <a name="annotated-x86-disassembly"></a>带批注的 x86 反汇编


## <span id="ddk_annotated_x86_disassembly_dbg"></span><span id="DDK_ANNOTATED_X86_DISASSEMBLY_DBG"></span>


以下部分将引导您完成反汇编示例。

### <a name="span-idsourcecodespanspan-idsourcecodespanspan-idsourcecodespansource-code"></a><span id="Source_Code"></span><span id="source_code"></span><span id="SOURCE_CODE"></span>源代码

下面是该函数将对其进行分析的代码。

```cpp
HRESULT CUserView::CloseView(void)
{
    if (m_fDestroyed) return S_OK;

    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);

    if (m_psv) {
        m_psb->EnableModelessSB(FALSE);
        if(m_pws) m_pws->ViewReleased();

        IShellView* psv;

        HWND hwndCapture = GetCapture();
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }

        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
        NotifyClients(m_psv, NOTIFY_CLOSING);
        m_fRecursing = FALSE;

        m_psv->UIActivate(SVUIA_DEACTIVATE);

        psv = m_psv;
        m_psv = NULL;

        ReleaseAndNull(&_pctView);

        if (m_pvo) {
            IAdviseSink *pSink;
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
                if (pSink == (IAdviseSink *)this)
                    m_pvo->SetAdvise(0, 0, NULL);
                pSink->Release();
            }

            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
        }

        if (psv) {
            psv->SaveViewState();
            psv->DestroyViewWindow();
            psv->Release();
        }

        m_hwndView = NULL;
        m_fHandsOff = FALSE;

        if (m_pcache) {
            GlobalFree(m_pcache);
            m_pcache = NULL;
        }

        m_psb->EnableModelessSB(TRUE);

        CancelPendingActions();
    }

    ReleaseAndNull(&_psf);

    if (fViewObjectChanged)
        NotifyViewClients(DVASPECT_CONTENT, -1);

    if (m_pszTitle) {
        LocalFree(m_pszTitle);
        m_pszTitle = NULL;
    }

    SetRect(&m_rcBounds, 0, 0, 0, 0);
    return S_OK;
}
```

### <a name="span-idassemblycodespanspan-idassemblycodespanspan-idassemblycodespanassembly-code"></a><span id="Assembly_Code"></span><span id="assembly_code"></span><span id="ASSEMBLY_CODE"></span>程序集代码

本部分包含带批注的反汇编示例。

函数使用该**ebp**注册，因为帧指针首先按如下所示：

```dbgcmd
HRESULT CUserView::CloseView(void)
SAMPLE!CUserView__CloseView:
71517134 55               push    ebp
71517135 8bec             mov     ebp,esp
```

这会设置框架以便函数可以访问其参数为正的偏移量，从**ebp**，和负偏移量为本地变量。

这是一个专用的 COM 接口上的方法，因此调用约定是 **\_ \_stdcall**。 这意味着从左到右推送参数 （在这种情况下，没有任何表），已推送"this"指针，且然后调用该函数。 因此，在进入该函数，在堆栈外观如下所示：

```dbgcmd
[esp+0] = return address
[esp+4] = this
```

后两个前面的说明的参数包括的可访问性：

```dbgcmd
[ebp+0] = previous ebp pushed on stack
[ebp+4] = return address
[ebp+8] = this
```

有关使用的函数**ebp**帧指针作为第一个推送的参数是在可访问\[ **ebp**+ 8\]; 后续参数是在连续访问更高版本DWORD 地址。

```dbgcmd
71517137 51               push    ecx
71517138 51               push    ecx
```

此函数需要只有两个局部堆栈变量，因此**sub esp**、 8 指令。 然后推送的值都可用作\[ **ebp**-4\]并\[ **ebp**-8\]。

有关使用的函数**ebp**堆栈本地变量作为帧指针，是访问从负偏移**ebp**注册。

```dbgcmd
71517139 56               push    esi
```

现在，编译器将保存在函数调用中保留所需的寄存器。 实际上，它将其保存在位和片段，交织在一起的实际代码的第一行。

```dbgcmd
7151713a 8b7508           mov     esi,[ebp+0x8]     ; esi = this
7151713d 57               push    edi               ; save another registers
```

它碰巧 CloseView 是一种方法是 12 基础对象中的偏移量处的视图状态上。 因此，**这**是类的视图状态的指针，但后可能另一个基类和混淆，它会在更加仔细地指定为 (ViewState\*)**这**。

```dbgcmd
    if (m_fDestroyed)
7151713e 33ff             xor     edi,edi           ; edi = 0
```

XORing 与其自身注册为零位调整它的标准方法。

```dbgcmd
71517140 39beac000000     cmp     [esi+0xac],edi    ; this->m_fDestroyed == 0?
71517146 7407             jz      NotDestroyed (7151714f)  ; jump if equal
```

**Cmp**指令比较两个值 （通过减去它们）。 **Jz**指令检查结果为零，这两个比较值，该值指示是否相等。

Cmp 指令比较两个值;后续 j 指令，跳转基于比较的结果。

```dbgcmd
    return S_OK;
71517148 33c0             xor     eax,eax           ; eax = 0 = S_OK
7151714a e972010000       jmp     ReturnNoEBX (715172c1) ; return, do not pop EBX
```

延迟保存更高版本在函数中，直到 EBX 注册编译器因此如果程序在此测试，然后退出路径上转到"早期 out"必须是一个不会还原 EBX。

```dbgcmd
    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);
```

交错执行的以下两行代码，因此应注意。

```dbgcmd
NotDestroyed:
7151714f 8d86c0000000     lea     eax,[esi+0xc0]    ; eax = &m_pdtgt
```

**逆转**指令计算内存访问的效果地址并将其存储在目标中。 不取消引用的实际内存地址。

逆转指令所采用的变量的地址。

```dbgcmd
71517155 53               push    ebx
```

之前已损坏，则应保存该 EBX 寄存器。

```dbgcmd
71517156 8b1d10195071     mov ebx,[_imp__ReleaseAndNull]
```

因为您将调用**ReleaseAndNull**通常情况下，它是缓存在 EBX 其地址的一个好办法。

```dbgcmd
7151715c 50               push    eax               ; parameter to ReleaseAndNull
7151715d 897dfc           mov     [ebp-0x4],edi     ; fViewObjectChanged = FALSE
71517160 ffd3             call    ebx               ; call ReleaseAndNull
    if (m_psv) {
71517162 397e74           cmp     [esi+0x74],edi    ; this->m_psv == 0?
71517165 0f8411010000     je      No_Psv (7151727c) ; jump if zero
```

请记住不久清 EDI 寄存器 EDI 是在函数调用中保留寄存器 (因此调用**ReleaseAndNull**未更改)。 因此，它仍包含值为零，而且可用来快速测试为零。

```dbgcmd
        m_psb->EnableModelessSB(FALSE);
7151716b 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151716e 57               push    edi               ; FALSE
7151716f 50               push    eax               ; "this" for callee
71517170 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
71517172 ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
```

上面的模式是比较的 COM 方法调用。

COM 方法调用是相当受欢迎，因此它是一个好办法了解可以识别它们。 具体而言，您应能够识别三种 IUnknown 方法直接从其 Vtable 偏移量：QueryInterface = 0，AddRef = 4，和发布 = 8。

```dbgcmd
        if(m_pws) m_pws->ViewReleased();
71517175 8b8614010000     mov     eax,[esi+0x114]   ; eax = this->m_pws
7151717b 3bc7             cmp     eax,edi           ; eax == 0?
7151717d 7406             jz      NoWS (71517185) ; if so, then jump
7151717f 8b08             mov     ecx,[eax]         ; ecx = m_pws->lpVtbl
71517181 50               push    eax               ; "this" for callee
71517182 ff510c           call    [ecx+0xc]         ; __stdcall ViewReleased
NoWS:
        HWND hwndCapture = GetCapture();
71517185 ff15e01a5071    call [_imp__GetCapture]    ; call GetCapture
```

间接调用通过全局函数是函数导入 Microsoft Win32 中的实现方式。 加载程序修复全局变量以指向目标的实际地址。 这是方便地帮留在那里您在调查崩溃的计算机。 查找导入的函数和在目标中的调用。 通常将具有一些导入的函数，可用于确定您的源代码中的位置的名称。

```dbgcmd
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }
7151718b 3bc7             cmp     eax,edi           ; hwndCapture == 0?
7151718d 7412             jz      No_Capture (715171a1) ; jump if zero
```

该函数返回值放在 EAX 中注册。

```dbgcmd
7151718f 8b4e44           mov     ecx,[esi+0x44]    ; ecx = this->m_hwnd
71517192 3bc1             cmp     eax,ecx           ; hwndCapture = ecx?
71517194 750b             jnz     No_Capture (715171a1) ; jump if not

71517196 57               push    edi               ; 0
71517197 57               push    edi               ; 0
71517198 6a1f             push    0x1f              ; WM_CANCELMODE
7151719a 51               push    ecx               ; hwndCapture
7151719b ff1518195071     call    [_imp__SendMessageW] ; SendMessage
No_Capture:
        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
715171a1 66818e0c0100000180 or    word ptr [esi+0x10c],0x8001 ; set both flags at once

        NotifyClients(m_psv, NOTIFY_CLOSING);
715171aa 8b4e20           mov     ecx,[esi+0x20]    ; ecx = (CNotifySource*)this.vtbl
715171ad 6a04             push    0x4               ; NOTIFY_CLOSING
715171af 8d4620           lea     eax,[esi+0x20]    ; eax = (CNotifySource*)this
715171b2 ff7674           push    [esi+0x74]        ; m_psv
715171b5 50               push    eax               ; "this" for callee
715171b6 ff510c           call    [ecx+0xc]         ; __stdcall NotifyClients
```

请注意，您必须从你自己的不同基类上调用方法时，更改"this"指针。

```dbgcmd
        m_fRecursing = FALSE;
715171b9 80a60d0100007f   and     byte ptr [esi+0x10d],0x7f
        m_psv->UIActivate(SVUIA_DEACTIVATE);
715171c0 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171c3 57               push    edi               ; SVUIA_DEACTIVATE = 0
715171c4 50               push    eax               ; "this" for callee
715171c5 8b08             mov     ecx,[eax]         ; ecx = vtbl
715171c7 ff511c           call    [ecx+0x1c]        ; __stdcall UIActivate
        psv = m_psv;
        m_psv = NULL;
715171ca 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171cd 897e74           mov     [esi+0x74],edi    ; m_psv = NULL
715171d0 8945f8           mov     [ebp-0x8],eax     ; psv = eax
```

第一个本地变量是**psv**。

```dbgcmd
        ReleaseAndNull(&_pctView);
715171d3 8d466c           lea     eax,[esi+0x6c]    ; eax = &_pctView
715171d6 50               push    eax               ; parameter
715171d7 ffd3             call    ebx               ; call ReleaseAndNull
        if (m_pvo) {
715171d9 8b86a8000000     mov     eax,[esi+0xa8]    ; eax = m_pvo
715171df 8dbea8000000     lea     edi,[esi+0xa8]    ; edi = &m_pvo
715171e5 85c0             test    eax,eax           ; eax == 0?
715171e7 7448             jz      No_Pvo (71517231) ; jump if zero
```

请注意，编译器推测性地准备好的地址**m\_pvo**成员，因为要使用它经常一段时间。 因此，具有方便的地址将导致较小的代码。

```dbgcmd
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
715171e9 8b08             mov     ecx,[eax]         ; ecx = m_pvo->lpVtbl
715171eb 8d5508           lea     edx,[ebp+0x8]     ; edx = &pSink
715171ee 52               push    edx               ; parameter
715171ef 6a00             push    0x0               ; NULL
715171f1 6a00             push    0x0               ; NULL
715171f3 50               push    eax               ; "this" for callee
715171f4 ff5120           call    [ecx+0x20]        ; __stdcall GetAdvise
715171f7 85c0             test    eax,eax           ; test bits of eax
715171f9 7c2c             jl      No_Advise (71517227) ; jump if less than zero
715171fb 33c9             xor     ecx,ecx           ; ecx = 0
715171fd 394d08           cmp     [ebp+0x8],ecx     ; _pSink == ecx?
71517200 7425             jz      No_Advise (71517227)
```

请注意，编译器得出的结论是，传入"this"参数不是必需的 （因为它很久以前存储的到 ESI 寄存器）。 因此，它作为本地变量 pSink 需要重复使用的内存。

如果该函数使用 EBP 帧，然后传入的参数从 EBP 到达正偏移量和本地变量放在负偏移量。 但是，在此情况下，编译器可以自由地重用该内存用于任何目的。

如果您要付密切注意，您将看到，编译器无法具有优化此代码更好地。 可能有延迟**逆转 edi \[esi + 0xa8\]** 直到后两个指令**推送 0x0**说明，将它们替换为**推送 edi**. 这会节省 2 个字节。

```dbgcmd
                if (pSink == (IAdviseSink *)this)
```

这些下一步的多个行是为了弥补这一事实，在C++，(IAdviseSink \*)**NULL**仍必须**NULL**。 因此，如果将"this"真正"(ViewState\*) NULL"，然后强制转换的结果应**NULL**和不 IAdviseSink IBrowserService 之间的距离。

```dbgcmd
71517202 8d46ec           lea     eax,[esi-0x14]    ; eax = -(IAdviseSink*)this
71517205 8d5614           lea     edx,[esi+0x14]    ; edx = (IAdviseSink*)this
71517208 f7d8             neg     eax               ; eax = -eax (sets carry if != 0)
7151720a 1bc0             sbb     eax,eax           ; eax = eax - eax - carry
7151720c 23c2             and     eax,edx           ; eax = NULL or edx
```

尽管 Pentium 具有条件移动指令，但基本 i386 体系结构不是，执行，因此编译器使用特定技术来模拟条件移动指令，而无需使任何跳转。

以下是条件计算的常规模式：

```dbgcmd
        neg     r
        sbb     r, r
        and     r, (val1 - val2)
        add     r, val2
```

**Neg r**设置携带标志，如果**r**为非零值，因为**neg**值减去零求反。 并且，减去从零开始时将生成借用 （设置执行进位） 减去一个非零值。 其还破坏了中的值**r**寄存器，但这是可接受因为您正准备是否仍要覆盖它。

下一步， **sbb r、 r**指令减去从其自身，这会始终导致零的值。 但是，它还减去携带 （借用） 位，因此最终结果是设置**r**为 0 或-1，具体取决于是否执行清除或分别设置。

因此， **sbb r、 r**设置**r**为零的原始值**r**是零，或为-1 时的原始值为非零值。

第三个指令执行一个掩码。 因为**r**注册为零则为-1，"this"提供任何一个以保留**r**零或更改**r**从-1 到 **(val1-val1)**，运算替换为-1 的任何值留出的原始值。

因此，结果的"和 r，(val1-val1)"是 r 如果设置为零的 r 的原始值为零，或"(val1-val2)"对 r 的原始值为非零值。

最后，添加**val2**到**r**，从而导致**val2**或者 **(val1-val2) + val2 = val1**。

因此，这一系列的说明进行操作的最终结果是设置**r**到**val2**如果最初是零，或者向**val1**如果是非零值。 这是程序集等效项**r = r？ val1: val2**。

在此特定情况下，可以看到**val2 = 0**并**val1 = (IAdviseSink\*) 这**。 (请注意，编译器省略最终**添加 eax，0**指令因为它不起作用。)

```dbgcmd
7151720e 394508           cmp     [ebp+0x8],eax ; pSink == (IAdviseSink*)this?
71517211 750b             jnz     No_SetAdvise (7151721e) ; jump if not equal
```

前面在本部分中，您将设置 EDI 为的地址**m\_pvo**成员。 要立即使用它。 您还之前清除 ECX 寄存器。

```dbgcmd
                    m_pvo->SetAdvise(0, 0, NULL);
71517213 8b07             mov     eax,[edi]         ; eax = m_pvo
71517215 51               push    ecx               ; NULL
71517216 51               push    ecx               ; 0
71517217 51               push    ecx               ; 0
71517218 8b10             mov     edx,[eax]         ; edx = m_pvo->lpVtbl
7151721a 50               push    eax               ; "this" for callee
7151721b ff521c           call    [edx+0x1c]        ; __stdcall SetAdvise
No_SetAdvise:
                pSink->Release();
7151721e 8b4508           mov     eax,[ebp+0x8]     ; eax = pSink
71517221 50               push    eax               ; "this" for callee
71517222 8b08             mov     ecx,[eax]         ; ecx = pSink->lpVtbl
71517224 ff5108           call    [ecx+0x8]         ; __stdcall Release
No_Advise:
```

所有这些 COM 方法调用应该很熟悉。

接下来两个语句的评估被交错进行。 不要忘记 EBX 包含的地址**ReleaseAndNull**。

```dbgcmd
            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
71517227 57               push    edi               ; &m_pvo
71517228 c745fc01000000   mov     dword ptr [ebp-0x4],0x1 ; fViewObjectChanged = TRUE
7151722f ffd3             call    ebx               ; call ReleaseAndNull
No_Pvo:
        if (psv) {
71517231 8b7df8           mov     edi,[ebp-0x8]     ; edi = psv
71517234 85ff             test    edi,edi           ; edi == 0?
71517236 7412             jz      No_Psv2 (7151724a) ; jump if zero
            psv->SaveViewState();
71517238 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
7151723a 57               push    edi               ; "this" for callee
7151723b ff5034           call    [eax+0x34]        ; __stdcall SaveViewState
```

以下是更多的 COM 方法调用。

```dbgcmd
            psv->DestroyViewWindow();
7151723e 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517240 57               push    edi               ; "this" for callee
71517241 ff5028           call    [eax+0x28]        ; __stdcall DestroyViewWindow
            psv->Release();
71517244 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517246 57               push    edi               ; "this" for callee
71517247 ff5008           call    [eax+0x8]         ; __stdcall Release
No_Psv2:
        m_hwndView = NULL;
7151724a 83667c00         and     dword ptr [esi+0x7c],0x0 ; m_hwndView = 0
```

运算带零的内存位置等同于将其设置为零，因为任何零值为零。 因为，即使它会慢些，它是比等效的短得多，编译器将使用此窗体**mov**指令。 （此代码进行了优化的大小，不速度。）

```dbgcmd
        m_fHandsOff = FALSE;
7151724e 83a60c010000fe   and     dword ptr [esi+0x10c],0xfe
        if (m_pcache) {
71517255 8b4670           mov     eax,[esi+0x70]    ; eax = m_pcache
71517258 85c0             test    eax,eax           ; eax == 0?
7151725a 740b             jz      No_Cache (71517267) ; jump if zero
            GlobalFree(m_pcache);
7151725c 50               push    eax               ; m_pcache
7151725d ff15b4135071     call    [_imp__GlobalFree]    ; call GlobalFree
            m_pcache = NULL;
71517263 83667000         and     dword ptr [esi+0x70],0x0 ; m_pcache = 0
No_Cache:
        m_psb->EnableModelessSB(TRUE);
71517267 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151726a 6a01             push    0x1               ; TRUE
7151726c 50               push    eax               ; "this" for callee
7151726d 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
7151726f ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
        CancelPendingActions();
```

若要调用**CancelPendingActions**，，必须从移动 (ViewState\*) 到 (CUserView\*) 这。 另请注意**CancelPendingActions**使用\_ \_thiscall 调用约定而不是\_ \_stdcall。 根据\_ \_thiscall，传递"this"指针在 ECX 寄存器，而不是在堆栈上传递。

```dbgcmd
71517272 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
71517275 e832fbffff       call CUserView::CancelPendingActions (71516dac) ; __thiscall
    ReleaseAndNull(&_psf);
7151727a 33ff             xor     edi,edi           ; edi = 0 (for later)
No_Psv:
7151727c 8d4678           lea     eax,[esi+0x78]    ; eax = &_psf
7151727f 50               push    eax               ; parameter
71517280 ffd3             call    ebx               ; call ReleaseAndNull
    if (fViewObjectChanged)
71517282 397dfc           cmp     [ebp-0x4],edi     ; fViewObjectChanged == 0?
71517285 740d             jz      NoNotifyViewClients (71517294) ; jump if zero
       NotifyViewClients(DVASPECT_CONTENT, -1);
71517287 8b46ec           mov     eax,[esi-0x14]    ; eax = ((CUserView*)this)->lpVtbl
7151728a 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
7151728d 6aff             push    0xff              ; -1
7151728f 6a01             push    0x1               ; DVASPECT_CONTENT = 1
71517291 ff5024           call    [eax+0x24]        ; __thiscall NotifyViewClients
NoNotifyViewClients:
    if (m_pszTitle)
71517294 8b8680000000     mov     eax,[esi+0x80]    ; eax = m_pszTitle
7151729a 8d9e80000000     lea     ebx,[esi+0x80]    ; ebx = &m_pszTitle (for later)
715172a0 3bc7             cmp     eax,edi           ; eax == 0?
715172a2 7409             jz      No_Title (715172ad) ; jump if zero
        LocalFree(m_pszTitle);
715172a4 50               push    eax               ; m_pszTitle
715172a5 ff1538125071     call   [_imp__LocalFree]
        m_pszTitle = NULL;
```

请记住，EDI 仍为零并且 EBX 是仍 （& m）\_pszTitle，因为这些寄存器将保留通过函数调用。

```dbgcmd
715172ab 893b             mov     [ebx],edi         ; m_pszTitle = 0
No_Title:
    SetRect(&m_rcBounds, 0, 0, 0, 0);
715172ad 57               push    edi               ; 0
715172ae 57               push    edi               ; 0
715172af 57               push    edi               ; 0
715172b0 81c6fc000000     add     esi,0xfc          ; esi = &this->m_rcBounds
715172b6 57               push    edi               ; 0
715172b7 56               push    esi               ; &m_rcBounds
715172b8 ff15e41a5071     call   [_imp__SetRect]
```

请注意，您无需"this"的值再，因此编译器将用**添加**指令而不是使用了另一个寄存器保存的址就地修改。 这是实际一个由于 Pentium u/v 借助管道传输，因为 v 管道可以进行算术运算，但无法解决计算的性能优势。

```dbgcmd
    return S_OK;
715172be 33c0             xor     eax,eax           ; eax = S_OK
```

最后，您还原系统要求保留、 清理堆栈，并返回到调用方，删除传入参数的寄存器。

```dbgcmd
715172c0 5b               pop     ebx               ; restore
ReturnNoEBX:
715172c1 5f               pop     edi               ; restore
715172c2 5e               pop     esi               ; restore
715172c3 c9               leave                     ; restores EBP and ESP simultaneously
715172c4 c20400           ret     0x4               ; return and clear parameters
```

 

 





