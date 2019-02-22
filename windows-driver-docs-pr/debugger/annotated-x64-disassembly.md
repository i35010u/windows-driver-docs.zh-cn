---
title: 带批注的 x64 反汇编
description: 带批注的 x64 反汇编
ms.assetid: 67930062-8a3a-460f-ae56-248d2a8e131e
keywords:
- x64 处理器，带批注的反汇编
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62993cca9e37a60ae1a6b674e15bc219f10404c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544116"
---
# <a name="annotated-x64-disassembly"></a>带批注的 x64 反汇编


## <span id="ddk_annotated_x64_disassembly_dbg"></span><span id="DDK_ANNOTATED_X64_DISASSEMBLY_DBG"></span>


下面的简单函数演示了 x64 调用约定。

```cpp
int Simple(int i, int j)
{
    return i*5 + j + 3;
}
```

这将编译为类似如下的代码：

```dbgcmd
01001080 lea     eax,[rdx+rcx*4]        ; eax = rdx+rcx*4
01001083 lea     eax,[rcx+rax+0x3]      ; eax = rcx+rax+3
01001087 ret
```

*我*并*j*中传递参数时**ecx**并**edx**注册，分别。 由于只有两个参数，该例程不完全使用堆栈。

生成的特定代码利用三个技巧，其中之一是特定于 x64:

1.  **逆转**操作可用于执行一系列简单的算术运算作为单个操作。 第一个指令存储*j + 我*\*中的第 4 **eax**，并将添加第二个说明*我*+ 3 表明汽车到结果中，总共*j* +*我*\*5 + 3。

2.  许多操作，例如加法和乘法，可以通过额外精度，然后截断为正确的精度。 在此情况下，代码使用 64 位加法和乘法。 我们可以安全地截断到 32 位的结果。

3.  在 x64 上的任何操作都自动输出到 32 位寄存器补零结果。 在这种情况下，输出到**eax**起的截断到 32 位的结果。

返回值，请传入**rax**注册。 在这种情况下，结果中已**rax**注册，因此该函数返回。

接下来我们考虑更复杂的函数，从而演示典型 x64 反汇编：

```cpp
HRESULT Meaningless(IDispatch *pdisp, DISPID dispid, BOOL fUnique, LPCWSTR pszExe)
{
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
    if (SUCCEEDED(hr)) {
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);
        if (SUCCEEDED(hr)) {
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {
                VARIANTARG rgvarg[2] = { 0 };
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {
                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }
        }
        pqa->Release();
    }
    return hr;
}
```

我们将通过此函数和等效的程序集行的行。

输入时，该函数的参数存储，如下所示：

-   **rcx** = *pdisp*。

-   **rdx** = *dispid*。

-   **r8** = *fUnique*。

-   **r9** = *pszExe*.

回想一下，在寄存器中传递的前四个参数。 由于此函数只需四个寄存器，都是在堆栈上传递。

程序集开始，如下所示：

```dbgcmd
Meaningless:
010010e0 push    rbx                    ; save
010010e1 push    rsi                    ; save
010010e2 push    rdi                    ; save
010010e3 push    r12d                   ; save
010010e5 push    r13d                   ; save
010010e7 push    r14d                   ; save
010010e9 push    r15d                   ; save
010010eb sub     rsp,0x2c0              ; reserve stack
010010f2 mov     rbx,r9                 ; rbx = pszExe
010010f5 mov     r12d,r8d               ; r12 = fUnique (zero-extend)
010010f8 mov     r13d,edx               ; r13 = dispid  (zero-extend)
010010fb mov     rsi,rcx                ; rsi = pdisp
```

此函数首先保存非易失寄存器，然后保留堆栈空间的本地变量。 然后将参数保存在非易失性寄存器中。 请注意，中间两个目标**mov**说明是 32 位寄存器，因此它们是隐式为 64 位扩展为零。

```dbgcmd
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
```

第一个参数**AssocCreate**是 128 位 CLSID 按值传递。 由于这不适合在 64 位寄存器，CLSID 复制到堆栈，并改为传递到堆栈位置的指针。

```dbgcmd
010010fe movdqu  xmm0,oword ptr [CLSID_QueryAssociations (01001060)]
01001106 movdqu  oword ptr [rsp+0x60],xmm0  ; temp buffer for first parameter
0100110c lea     r8,[rsp+0x58]          ; arg3 = &pqa
01001111 lea rdx,[IID_IQueryAssociations (01001070)] ; arg2 = &IID_IQueryAssociations
01001118 lea     rcx,[rsp+0x60]         ; arg1 = &temporary
0100111d call qword ptr [_imp_AssocCreate (01001028)] ; call
```

**Movdqu**指令将转移 128 位值，与 **xmm * * * n*注册。 在此情况下，程序集代码使用它来复制到堆栈的 CLSID。 对 CLSID 的指针传入**r8**。 其他两个参数中传递**rcx**并**rdx**。

```dbgcmd
    if (SUCCEEDED(hr)) {

01001123 test    eax,eax
01001125 jl      ReturnEAX (01001281)
```

代码检查以查看返回的值是否成功完成。

```dbgcmd
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);

0100112b mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001130 mov     rax,[rcx]              ; rax = pqa.vtbl
01001133 xor     r14d,r14d              ; r14 = 0
01001136 mov     [rsp+0x20],r14         ; arg5 = 0
0100113b xor     r9d,r9d                ; arg4 = 0
0100113e mov     r8,rbx                 ; arg3 = pszExe
01001141 mov     r15d,0x2               ; r15 = 2 (for later)
01001147 mov     edx,r15d               ; arg2 = 2 (ASSOCF_INIT_BY_EXENAME)
0100114a call    qword ptr [rax+0x18]   ; call Init method
```

这是使用 c + + vtable 的间接函数调用。 **这**指针传入**rcx**作为第一个参数。 前三个参数将传入寄存器，而在堆栈上传递的最后一个参数。 该函数会保留在寄存器中传递，因此在开始第五个参数的参数的 16 个字节**rsp**+ 0x20。

```dbgcmd
        if (SUCCEEDED(hr)) {

0100114d mov     ebx,eax                ; ebx = hr
0100114f test    ebx,ebx                ; FAILED?
01001151 jl      ReleasePQA (01001274)  ; jump if so
```

此程序集语言代码将保存在结果**ebx**，并检查它是否成功代码。

```dbgcmd
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {

01001157 mov     dword ptr [rsp+0x50],0x104 ; cchName = MAX_PATH
0100115f mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001164 mov     rax,[rcx]              ; rax = pqa.vtbl
01001167 lea     rdx,[rsp+0x50]         ; rdx = &cchName
0100116c mov     [rsp+0x28],rdx         ; arg6 = cchName
01001171 lea     rdx,[rsp+0xb0]         ; rdx = &wszName[0]
01001179 mov     [rsp+0x20],rdx         ; arg5 = &wszName[0]
0100117e xor     r9d,r9d                ; arg4 = 0
01001181 mov     r8d,0x4                ; arg3 = 4 (ASSOCSTR_FRIENDLYNAME)
01001187 xor     edx,edx                ; arg2 = 0
01001189 call    qword ptr [rax+0x20]   ; call GetString method
0100118c mov     ebx,eax                ; ebx = hr
0100118e test    ebx,ebx                ; FAILED?
01001190 jl      ReleasePQA (01001274)  ; jump if so
```

再次重申，我们设置的参数和调用函数，然后测试成功的返回值。

```dbgcmd
                VARIANTARG rgvarg[2] = { 0 };

01001196 lea     rdi,[rsp+0x82]         ; rdi = &rgvarg
0100119e xor     eax,eax                ; rax = 0
010011a0 mov     ecx,0x2e               ; rcx = sizeof(rgvarg)
010011a5 rep     stosb                  ; Zero it out
```

在 x64 上的缓冲区清零的惯用方法是 x86 相同。

```dbgcmd
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {

010011a7 mov     word ptr [rsp+0x80],0x8 ; V_VT(&rgvarg[0]) = VT_BSTR
010011b1 lea     rcx,[rsp+0xb0]         ; arg1 = &wszName[0]
010011b9 call    qword ptr [_imp_SysAllocString (01001010)] ; call
010011bf mov     [rsp+0x88],rax         ; V_BSTR(&rgvarg[0]) = result
010011c7 test    rax,rax                ; anything allocated?
010011ca je      OutOfMemory (0100126f) ; jump if failed

                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);

010011d0 lea     rax,[lCounter (01002000)]
010011d7 mov     ecx,0x1
010011dc lock    xadd [rax],ecx             ; interlocked exchange and add
010011e0 add     ecx,0x1
```

**InterlockedIncrement**直接为机器代码编译。 **锁定 xadd**指令执行原子交换，并添加。 最终结果存储在**ecx**。

```dbgcmd
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;

010011e3 mov     word ptr [rsp+0x98],0x3    ; V_VT(&rgvarg[1]) = VT_I4;
010011ed mov     eax,r14d                   ; rax = 0 (r14d is still zero)
010011f0 test    r12d,r12d                  ; fUnique set?
010011f3 cmovne  eax,ecx                    ; if so, then set rax=lCounter
010011f6 mov     [rsp+0xa0],eax             ; V_I4(&rgvarg[1]) = ...
```

由于支持 x64 **cmov**指令 **？:** 构造可编译而无需使用跳转。

```dbgcmd
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;

010011fd lea     rax,[rsp+0x80]             ; rax = &rgvarg[0]
01001205 mov     [rsp+0x60],rax             ; dp.rgvarg = rgvarg
0100120a mov     [rsp+0x70],r15d            ; dp.cArgs = 2 (r15 is still 2)
0100120f mov     [rsp+0x68],r14             ; dp.rgdispidNamedArgs = NULL
01001214 mov     [rsp+0x74],r14d            ; dp.cNamedArgs = 0
```

此代码将初始化 DISPPARAMS 的成员的其余部分。 请注意，编译器将重用以前使用 CLSID 的堆栈上的空间。

```dbgcmd
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);

01001219 mov     rax,[rsi]                  ; rax = pdisp.vtbl
0100121c mov     [rsp+0x40],r14             ; arg9 = 0
01001221 mov     [rsp+0x38],r14             ; arg8 = 0
01001226 mov     [rsp+0x30],r14             ; arg7 = 0
0100122b lea     rcx,[rsp+0x60]             ; rcx = &dp
01001230 mov     [rsp+0x28],rcx             ; arg6 = &dp
01001235 mov     word ptr [rsp+0x20],0x1    ; arg5 = 1 (DISPATCH_METHOD)
0100123c xor     r9d,r9d                    ; arg4 = 0
0100123f lea     r8,[GUID_NULL (01001080)]  ; arg3 = &IID_NULL
01001246 mov     edx,r13d                   ; arg2 = dispid
01001249 mov     rcx,rsi                    ; arg1 = pdisp
0100124c call    qword ptr [rax+0x30]       ; call Invoke method
0100124f mov     ebx,eax                    ; hr = result
```

代码随后设置参数和调用**Invoke**方法。

```dbgcmd
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);

01001251 lea     rcx,[rsp+0x80]             ; arg1 = &rgvarg[0]
01001259 call    qword ptr [_imp_VariantClear (01001018)]
0100125f lea     rcx,[rsp+0x98]             ; arg1 = &rgvarg[1]
01001267 call    qword ptr [_imp_VariantClear (01001018)]
0100126d jmp     ReleasePQA (01001274)
```

代码完成的当前分支的条件，并跳过**其他**分支。

```dbgcmd
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }

OutOfMemory:
0100126f mov     ebx,0x8007000e             ; hr = E_OUTOFMEMORY
        pqa->Release();
ReleasePQA:
01001274 mov     rcx,[rsp+0x58]             ; arg1 = pqa
01001279 mov     rax,[rcx]                  ; rax = pqa.vtbl
0100127c call    qword ptr [rax+0x10]       ; release
```

**其他**分支。

```dbgcmd
    return hr;
}

0100127f mov     eax,ebx                    ; rax = hr (for return value)
ReturnEAX:
01001281 add     rsp,0x2c0                  ; clean up the stack
01001288 pop     r15d                       ; restore
0100128a pop     r14d                       ; restore
0100128c pop     r13d                       ; restore
0100128e pop     r12d                       ; restore
01001290 pop     rdi                        ; restore
01001291 pop     rsi                        ; restore
01001292 pop     rbx                        ; restore
01001293 ret                                ; return (do not pop arguments)
```

返回值存储在**rax**，且返回前还原非易失寄存器是。

 

 





