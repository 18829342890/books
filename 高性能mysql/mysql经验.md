##刷大量数据

- 需要多线程处理，update很多记录，磁盘i/o时间太长，单线程的话会很慢
- 多线程需要考虑不能重复处理
- 需要考虑db每秒能接受多少update
- 每个线程需要sleep，太快了会把db搞挂，基于上面的条件和数据总数量，给出一个合理的线程数和sleep的微妙数
- 不能导致锁表
- 刷的时候关注db的性能
- 可以记录开始时间和结束时间，处理成功和处理失败的单独记录。
- 支持处理失败的进行重试
- 不能调接口，会把线上的接口调蹦的
- 可以多次运行脚本而不会有问题
- 需考虑数据是否需要备份，是否需要指出数据回滚