----readme file for ques1----

->Here first we go to include/linux then in sched.h in sched_entity we define struct {
u64 delay;
u64 print_exec_start;
} 
->then in kernel/sched/core.c on line 300: we add
	p-> se.delay=0;
	p->se.print_exec_start=0;
->then in kernel/sched/fair.c we add
	curr->runtime+=curr->delay;
->after this we just add our system call in systable and our system call code is

SYSCALL_DEFINE1(mohd,int,pid){
    struct pid *id;

	struct task_struct *st;
    id = find_get_pid(pid);
    st = pid_task(id, PIDTYPE_PID);
	
	st->se.time=(5000000);
	printk("Delayed by 5ms \n");
	printk("time takn to complete: %lld",st->se.sum_exec_runtime);
	return 0;

}
