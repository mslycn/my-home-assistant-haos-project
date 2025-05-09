Get a NUC, and get Proxmox onto the NUC, and then you can get the “appliance like experience" running a HAOS VM under Proxmox, you can also get all kinds of different containers.

在NUC上装个PVE，群晖、飞牛nas、ikuai、istoreos、haos等同时运行，X86的地位就非常凸显了

## Options
- I have home assistant running in a VM on proxmox.

## Guide

Installing Proxmox VE 8



- Installing Home Assistant OS using Proxmox 8
https://community.home-assistant.io/t/installing-home-assistant-os-using-proxmox-8/201835/572

- Installing Home Assistant docker using Proxmox 8 on intel NUC
https://www.cnblogs.com/yixueli/p/12548972.html


esxi

8G内存，intel 3215U，装esxi，分配2G内存加2核cpu，跑第一个，CPU直接跑满，不过看官网文档，可以外挂Coral Accelerator ，想搞个试一下，没地方买
第2和第3个，3秒检测一次，CPU在60%左右