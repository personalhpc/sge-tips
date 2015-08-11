# sge-tips
Tips for sun grid engine management

```bash
ps -A | grep sge
```
shoud return at least two lines, one with sge_qmaster (sge server deamon) and sge_execd (client)
```bash
 1655 ?        00:00:00 sge_qmaster
 1667 ?        00:00:00 sge_execd
```

If `sge_qmaster` is not here, start it with `sudo sge_qmaster`
If `sge_execd` is not here, start it with `sudo sge_execd`

Full information about the queue(s):
```bash
qstat -f -u "*"
```
which is especially interesting is the state of the queue. To get more information about a state, for instance state `E`:
```bash
qstat -explain E
```

If some problem comes from job 3151:
```bash
qstat -j 3151
```

delete the job.

The queue state is dropped for some reason but your cleaning won't be sufficient to reinit the state. You have to do it manually. If queue name is main.q, then:
```bash
qmod -cq main.q
```

Verify queue state is now ok with `qstat -f -u "*"`
If not sufficient to make everything clean, restart manually everything:
```bash
sudo service gridengine-master restart
```
