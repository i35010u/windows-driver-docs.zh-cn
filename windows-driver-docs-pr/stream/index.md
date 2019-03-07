---
title: 流媒体设备驱动程序设计指南
description: 流媒体设备驱动程序设计指南
ms.assetid: 321edd72-4f6a-4eaf-85bf-3b36680a522c
keywords:
  - 流媒体 WDK
  - 媒体流式处理 WDK
  - 数据流式处理 WDK
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="streaming-media-device-driver-design-guide"></a>流媒体设备驱动程序设计指南

使用本部分中的指南为对视频和音频进行流式处理的设备（例如网络摄像头和数码摄像机）设计和实现驱动程序。

## <a name="in-this-section"></a>本部分中的内容

- [在不使用共同安装程序的情况下为 USB 设备更新设备固件](device-firmware-update-for-usb-devices-without-using-a-co-installer.md)
- [USB 视频类 (UVC) 相机实现指南](uvc-camera-implementation-guide.md)
- [Frame Server 自定义媒体源](frame-server-custom-media-source.md)
- [360 相机视频捕获](360-camera-video-capture.md)（Windows 10 版本 1803 的新功能）
- [相机内部函数](camera-intrinsics.md)
- [适用于 UVC 设备的 DShow 桥实现指南](dshow-bridge-implementation-guidance-for-usb-video-class-devices.md)
- [通用相机驱动程序的相机类 INF 文件设置](camera-driver-inf-file-class-setting.md)（Windows 10 版本 1709 的新功能）
- [USB 视频类 (UVC) 驱动程序实现清单](uvc-driver-implementation-checklist.md)（Windows 10 版本 1703 的新功能）
- [相机设备方向](camera-device-orientation.md)
- [AVStream 微型驱动程序](avstream-minidrivers-design-guide.md)
- [Windows 2000 内核流式处理模型设计指南](windows-2000-kernel-streaming-model-design-guide.md)
- [内核流式处理代理插件](kernel-streaming-proxy-plug-ins-design-guide.md)
- [流媒体示例](streaming-media-samples.md)
- [适用于 OEM 的 Windows 10 内置相机应用设置指南](oem-guidance-on-settings-for-the-windows-10-in-box-camera-app.md)
- [视频防抖动注册表设置](oem-guidance-on-registry-keys-for-video-stabilization.md)
- [扩展的相机控件](standardized-extended-controls-.md)（Windows 10 版本 1607 的更新功能）
- [相机驱动程序“引入”指南](windows-hello-camera-driver-bring-up-guide.md)（Windows 10 版本 1607 的新功能）
- [适用于 Windows 10 的通用相机驱动程序设计指南](windows-10-technical-preview-camera-drivers-design-guide.md)
- [AVStream 属性集](avstream-property-sets.md)
- [广播驱动程序体系结构属性、事件和方法集](broadcast-driver-architecture-property--event--and-method-sets.md)
- [广播驱动程序体系结构常量](broadcast-driver-architecture-constants.md)
- [编码器属性集](encoder-property-sets.md)
- [编码器事件](encoder-events.md)
- [AV/C 协议驱动程序函数代码](av-c-protocol-driver-function-codes.md)
- [AV/C 流式处理协议驱动程序函数代码](av-c-streaming-protocol-driver-function-codes.md)
- [AV/C 流式处理常量](av-c-streaming-constants.md)
- [视频捕获微型驱动程序属性集](video-capture-minidriver-property-sets.md)
- [视频捕获微型驱动程序事件集](video-capture-minidriver-event-sets.md)
- [设备转换管理器事件](device-mft-events.md)
- [内核流式处理拓扑节点](kernel-streaming-topology-nodes.md)
- [内核流式处理接口集](kernel-streaming-interface-sets.md)
- [内核流式处理事件集](kernel-streaming-event-sets.md)
- [内核流式处理方法集](kernel-streaming-method-sets.md)
- [流式处理类 SRB 参考](stream-class-srb-reference.md)
- [DVD 解码器微型驱动程序属性集](dvd-decoder-minidriver-property-sets.md)
- [DVD 解码器微型驱动程序事件集](dvd-decoder-minidriver-event-sets.md)
- [COM 接口](com-interfaces.md)

## <a name="related-sections"></a>相关章节

- [流媒体 DDI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream)
