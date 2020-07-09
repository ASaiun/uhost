# 2020-06 实例升级公告

出于对云主机稳定性、数据安全性的考量，UCloud将对底层硬件寿命较长的云主机实例进行持续在线升级。

具体操作为：

  - 将硬件寿命较长（多数CPU平台为Intel Ivybridge, Haswell, Broadwell）的物理宿主机上的云主机实例迁移到最新的物理宿主机（CPU平台为Intel Cascadelake）；
  - 将以SATA为介质的普通本地盘在线升级到以NVMe SSD为介质的SSD云盘

升级将分多个阶段，多个批次进行。每个阶段相当于1次云主机**在线热迁移**，基本无感知，且升级后实例**费用不变**。

具体升级进度由UCloud统一规划，涉及迁移升级的主机会在迁移前24小时通告。详情请咨询您的服务经理/技术支持。

## FAQ：

**Q: 是否是升级到最新的快杰型云主机？**

A: 此次升级到的机型不是快杰型，而是通用型（Cascadelake）+SSD云盘。通用型（Cascadelake）这种实例仅能被升级，暂不会开放申请。

由于快杰型的操作系统需要支撑高性能的网络与存储，依赖实例的操作系统内核为高版本内核（≥4.14）。由于我们无法直接升级您的操作系统OS，故仅支持升级到最新CPU平台的通用型主机。若希望得到快杰型更优的性能/价格，建议新购快杰云主机，通过应用层迁移方式切换业务。

附 通用型Cascadelake与快杰型的比对：

| | 通用型（Cascadelake） | 快杰型 | 
| ----------- | -------------------- | ---------------- |
| CPU	| Intel Cascadelake	| Intel Cascadelake 或 AMD |
| 网络 | 30W PPS <br/> 可开启网络增强提升至100W PPS | 1000W PPS|
| 存储 | SSD云盘（最大2.6W IOPS）|	RSSD云盘（最大120W IOPS） |
| 操作系统需求 | 任意 | 高内核（内核版本≥4.19） |
| 可新购？| 否 | 是 |

**Q：迁移对业务有影响么？**

迁移过程中会发生2次500ms的网络闪断，此外理论无影响。

**Q：迁移后，性能相比迁移前会有如何影响？**

由于迁移分多阶段进行，在所有阶段最终完成时，CPU性能与存储性能均会得到一定程度提升。

CPU性能：由于CPU从2014/2015年款的IvyBridge/Haswell/Broadwell升级到了2019款的Cascadelake，因此计算性能会获得最大20%的直接提升。

存储性能：由于从以SATA-HDD为介质的本地普通盘升级到了以NVMe SSD为介质的云盘，最大随机IO/顺序吞吐性能都会得到提升，且性能会更稳定可靠。

附录：SSD云盘性能与本地普通盘性能对比

| | 普通本地盘 | SSD云盘 |
| ----------- | -------------------- | ---------------- |
| 随机IO | 峰值8000 | 稳定min{1200+30 * 容量，24000} |
| 顺序IO (MB/s) |  峰值150 | 稳定min{80+0.5 * 容量，260}MBps
| 延迟 |	0.3ms | 0.5-3ms |

详情可参考 [主机磁盘简介](/uhost/introduction/disk)

**Q:这次升级还有哪些能力提升？**

由于从本地盘升级到了云盘，宿主机宕机时，云主机能执行快速漂移并重新开机，恢复速度从原本影响30分钟以上，降低到5分钟以内。

且数据从原来的本地盘两副本提升到云盘的三副本机制，数据安全性更高。

**Q：迁移后，新实例的价格在下次续费时会变化么？**

价格不会发生变化，只要实例不被删除，将保持迁移前的价格。

但仅此次升级的能享受”价格不变“的优惠，新购机型的普通本地盘与SSD云盘仍会有价格差异。具体价格请参考控制台。