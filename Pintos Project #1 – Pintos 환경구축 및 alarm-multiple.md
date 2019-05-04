**Pintos Project #1 – Pintos** **환경구축 및 alarm-multiple ** 



**목차**

**I.**         **Alarm-multiple** **실행화면 출력 및 설명**

**II.**       **Pintos** **의 main함수 와 실행경로**

\-    **중요 함수1)~15)**

**III.**     **자료구조 설명**

**IV.**     **함수설명**

\-    **1)~15)** **중요함수 설명**

 



 

**I.**              **Alarm-multiple** **실행화면:**

 **pintos-v  -- run alarm-multiple****을 실행했을 때 화면은 다음과 같다.**

 

 

**f literal control characters in variable names is deprecated at /home/pintos/pintos/src/utils/pintos line 911.**

**Prototype mismatch: sub main::SIGVTALRM () vs none at /home/pintos/pintos/src/utils/pintos line 935.**

**Constant subroutine SIGVTALRM redefined at /home/pintos/pintos/src/utils/pintos line 927.**

**warning: can't find squish-pty, so terminal input will fail**

**bochs -q**

**========================================================================**

​                       **Bochs x86 Emulator 2.6.2**

​                **Built from SVN snapshot on May 26, 2013**

​                  **Compiled on Feb 19 2019 at 17:39:30**

**========================================================================**

**00000000000i[     ] reading configuration from bochsrc.txt**

**00000000000e[     ] bochsrc.txt:8: 'user_shortcut' will be replaced by new 'keyboard' option.**

**00000000000i[     ] installing nogui module as the Bochs GUI**

**00000000000i[     ] using log file bochsout.txt**

**PiLo hda1**

**Loading...........**

**Kernel command line: run alarm-multiple**

**Pintos booting with 4,096 kB RAM...**

**383 pages available in kernel pool.**

**383 pages available in user pool.**

**Calibrating timer...  204,600 loops/s.**

**Boot complete.**

**Executing 'alarm-multiple':**

**(alarm-multiple) begin**

**(alarm-multiple) Creating 5 threads to sleep 7 times each.**

**(alarm-multiple) Thread 0 sleeps 10 ticks each time,**

**(alarm-multiple) thread 1 sleeps 20 ticks each time, and so on.**

**(alarm-multiple) If successful, product of iteration count and**

**(alarm-multiple) sleep duration will appear in nondescending order.**

**(alarm-multiple) thread 0: duration=10, iteration=1, product=10**

**(alarm-multiple) thread 0: duration=10, iteration=2, product=20**

**(alarm-multiple) thread 1: duration=20, iteration=1, product=20**

**(alarm-multiple) thread 0: duration=10, iteration=3, product=30**

**(alarm-multiple) thread 2: duration=30, iteration=1, product=30**

**(alarm-multiple) thread 1: duration=20, iteration=2, product=40**

**(alarm-multiple) thread 3: duration=40, iteration=1, product=40**

**(alarm-multiple) thread 0: duration=10, iteration=4, product=40**

**(alarm-multiple) thread 4: duration=50, iteration=1, product=50**

**(alarm-multiple) thread 0: duration=10, iteration=5, product=50**

**(alarm-multiple) thread 2: duration=30, iteration=2, product=60**

**(alarm-multiple) thread 0: duration=10, iteration=6, product=60**

**(alarm-multiple) thread 1: duration=20, iteration=3, product=60**

**(alarm-multiple) thread 0: duration=10, iteration=7, product=70**

**(alarm-multiple) thread 3: duration=40, iteration=2, product=80**

**(alarm-multiple) thread 1: duration=20, iteration=4, product=80**

**(alarm-multiple) thread 2: duration=30, iteration=3, product=90**

**(alarm-multiple) thread 1: duration=20, iteration=5, product=100**

**(alarm-multiple) thread 4: duration=50, iteration=2, product=100**

**(alarm-multiple) thread 1: duration=20, iteration=6, product=120**

**(alarm-multiple) thread 2: duration=30, iteration=4, product=120**

**(alarm-multiple) thread 3: duration=40, iteration=3, product=120**

**(alarm-multiple) thread 1: duration=20, iteration=7, product=140**

**(alarm-multiple) thread 2: duration=30, iteration=5, product=150**

**(alarm-multiple) thread 4: duration=50, iteration=3, product=150**

**(alarm-multiple) thread 3: duration=40, iteration=4, product=160**

**(alarm-multiple) thread 2: duration=30, iteration=6, product=180**

**(alarm-multiple) thread 3: duration=40, iteration=5, product=200**

**(alarm-multiple) thread 4: duration=50, iteration=4, product=200**

**(alarm-multiple) thread 2: duration=30, iteration=7, product=210**

**(alarm-multiple) thread 3: duration=40, iteration=6, product=240**

**(alarm-multiple) thread 4: duration=50, iteration=5, product=250**

**(alarm-multiple) thread 3: duration=40, iteration=7, product=280**

**(alarm-multiple) thread 4: duration=50, iteration=6, product=300**

**(alarm-multiple) thread 4: duration=50, iteration=7, product=350**

**(alarm-multiple) end**

**Execution of 'alarm-multiple' complete.**

 

 

 

**/home/pintos/src/utils** **에 있는 pintos파일에 핀토스의 정의들이 들어가 있다.**

 

**커널 명령어는 run alarm-multiple이고 4MB크기의 램이 핀토스 부팅에 할당된다. 383페이지의 tcb가 유저와 커널스레드에 할당가능하다.**

**204,600** **번 동안 타이머가 작동되고, 부팅이 완료된다. 부팅이 완료되면 alarm-multiple이 실행된다.** 

 

**/home/pintos/src/tests/thread** **에 alarm-multiple.ck 파일이 있다.** 

**# -\*- perl -\*-**

**Use test::tests;**

**Use tests::threas::alarm;**

**Check_alarm (7);**

 

**위처럼 작성되어 있다. Check_alarm에 7을 입력하여 결과를 확인하는 파일이다.** 

 

**스레드 5개가 만들어지고  각각 7번 작동한다. 스레드 0은 10 ticks마다 작동하고 스레드 1은 20 ticks마다 작동한다. 스레드 2는 30 ticks마다 작동하고, 스레드 3은 40 ticks마다 작동한다. 그리고 스레드 4는 50ticks마다 작동한다. 모든 스레드가 작동을 7번 하면 알람이 종료된다.**

**스레드 0은 10의 배수인 10,20,30,40,50,60,70에 타이머를 작동시키고, 스레드 1은 20의 배수인 20,40,60,80,100,120,140에 타이머를 작동시킨다. 스레드 2는 30의 배수인 30,60,90,120,150,180,210에 타이머를 작동시키고, 스레드3은 40,80,120,160,200,240,280에 타이머를 작동시킨다. 스레드 4는 50의 배수인 50,100,150,200,250,300,350에 타이머를 작동시킨다**

 

**II.**            **Pintos** **의 main함수와 실행경로**

\-     **pintos** **운영체제가 부팅을 시작하면 커널을 실행시킨다. 커널을 만들기 위해 init.c가 실행된다.** 

\-      

**메인함수를 보면 다음과 같다.**

 

int main (void) NO_RETURN;

 

/* Pintos main program. */

int

main (void)

{

  char **argv;

 

  /* Clear BSS. */  

  bss_init ();                              **//1)** **커널이 사용하는 bss 영역 초기화**

 

  /* Break command line into arguments and parse options. */

  argv = read_command_line ();       **//2)command line** **으로 입력되는 것을 argument vector에 저장**

  argv = parse_options (argv);         **//3)** **파싱을 해서 argv에 다시 저장함**

 

  /* Initialize ourselves as a thread so we can use locks,

​     then enable console locking. */

  thread_init ();                           **//4)** **자기자신을 thread로 만듦, 최초의 thread** 

  console_init ();                        **//** **콘솔 초기화**

 

  /* Greet user. */

  printf ("Pintos booting with %'"PRIu32" kB RAM...\n",

​          init_ram_pages * PGSIZE / 1024);

 

  /* Initialize memory system. */

  palloc_init (user_page_limit);         **//5)** **메모리를**

  malloc_init ();                       	    **//6)** **초기화하는** 

  paging_init ();                       	    **//7)** **함수들**

 

  /* Segmentation. */

\#ifdef USERPROG

  tss_init ();

  gdt_init ();

\#endif

 

  /* Initialize interrupt handlers. */

  intr_init ();                               **//8)** **인터럽트를 초기화**

  timer_init ();                             **//9)** **타이머를 초기화**

  kbd_init ();                              **//10)** **키보드 초기화**

  input_init ();                            **//11)** **입력 초기화**

\#ifdef USERPROG

  exception_init ();

  syscall_init ();

\#endif

 

  /* Start thread scheduler and enable interrupts. */

  thread_start ();              **//12) idle** **을 만들고 인터럽트를 활성화함 스케줄링이 가능해짐**

  serial_init_queue ();        **//13)** **스케줄링을 위해 레디큐를 만듦**

  timer_calibrate ();           **//14)** **스케줄링을 위해 타이머를 시작함.**

 

\#ifdef FILESYS

  /* Initialize file system. */

  ide_init ();

  locate_block_devices ();

  filesys_init (format_filesys);

\#endif

 

  printf ("Boot complete.\n");

  

  /* Run actions specified on kernel command line. */

  run_actions (argv);         **//15)** **동작을 실행함. 이번 과제에서는 run alarm-multiple이 된다.**

 

  /* Finish up. */

  shutdown ();

  thread_exit ();

}

 

 

**//****소스파일**

\- ‘loader.S’

\- ‘loader.h’

커널 로더. 512 바이트의 코드 및 데이터를 PC로 어셈블 BIOS는 메모리에로드되고 커널은 메모리에로드되며, 기본 프로세서 초기화를 수행하고 커널 시작 부분으로 이동합니다.

 

 

\- ‘kernel.lds.S’

커널을 링크하는 데 사용되는 링커 스크립트. 커널의로드 주소를 설정하고 'start.S'가 커널 이미지의 맨 처음에 오도록 정렬합니다.

 

 \- ‘start.S’

메인 함수로 점프하는 함수

 

\- ‘init.c’

\- ‘init.h’ 

main (), 커널의 "main program"을 포함한 커널 초기화. 적어도 초기화되는 것을 보려면 main ()을 살펴야합니다.

 

 

\- ‘thread.c’

\- ‘thread.h’
 기본 스레드 지원. 많은 작업이이 파일에서 수행됩니다. 'thread.h'는 네 개의 프로젝트 모두에서 수정할 가능성이 높은 struct thread를 정의합니다.

 

 

  \- ‘switch.S’ 

\- ‘switch.h’
 스레드 전환을위한 어셈블리 언어 루틴. 이미 위에서 논의한 바 있습니다.

 

  \- ‘palloc.c’ 

\- ‘palloc.h’

4KB 페이지의 배수로 시스템 메모리를 넘겨주는 페이지 할당 자.

 

\-  ‘malloc.c’

\- ‘malloc.h’

커널을위한 malloc ()과 free ()의 간단한 구현.

 

  \- ‘interrupt.c’

\- ‘interrupt.h’

기본 인터럽트 처리 및 인터럽트를 켜고 끄는 기능.

 

  \- ‘intr-stubs.S’

\- ‘intr-stubs.h’


 low level 인터럽트 처리를위한 어셈블리 코드.

 

\- ‘synch.c’


 synch.h '기본 동기화 기본 요소 : 세마포, 잠금, 조건 변수 및 최적화 장벽. 네 가지 프로젝트 모두에서 동기화에 사용해야합니다.

 

\- ‘vaddr.h’


 'pte.h'가상 주소와 페이지 테이블 항목을 다루기 위한 함수와 매크로. 이것들은 프로젝트 3에서 당신에게 더 중요 할 것입니다. 'flags.h'80x86 "flags"레지스터에 몇 비트를 정의하는 매크로

 

 

**III.**          **자료구조**

**1)**   **스레드의 상태**

 

enum thread_status

  {

​    THREAD_RUNNING,     /* Running thread. */

​    THREAD_READY,       /* Not running but ready to run. */

​    THREAD_BLOCKED,     /* Waiting for an event to trigger. */

​    THREAD_DYING        /* About to be destroyed. */

};

 

**스레드의 상태는 running, ready, blocked, dying이 있다. new상태가 없는 이유는 new상태에서 long-term job 스케줄러에 의해 ready큐에 들어가는 상황에서 스레드가 생성되기 때문에 new상태를 제외한 running, ready, blocked(waiting), dying(terminated)가 있다.**

 

**2)**   **스레드의 우선순위**

 

typedef int tid_t;

\#define TID_ERROR ((tid_t) -1)          /* Error value for tid_t. */

 

/* Thread priorities. */

\#define PRI_MIN 0                       /* Lowest priority. */

\#define PRI_DEFAULT 31                  /* Default priority. */

\#define PRI_MAX 63                      /* Highest priority. */

 

**스레드의 우선순위는 0부터 63까지 있다. 0이 가장 낮은 우선순위이고, 63은 가장 높은 우선순위 이다. 31은 default값이다.** 

 

**3)**   **스레드 구조체의 요소들**

 

struct thread

  {

​    /* Owned by thread.c. */

​    tid_t tid;                          /* Thread identifier. */

​    enum thread_status status;          /* Thread state. */

​    char name[16];                      /* Name (for debugging purposes). */

​    uint8_t *stack;                     /* Saved stack pointer. */

​    int priority;                       /* Priority. */

​    struct list_elem allelem;           /* List element for all threads list. */

 

​    /* Shared between thread.c and synch.c. */

​    struct list_elem elem;              /* List element. */

 

\#ifdef USERPROG

​    /* Owned by userprog/process.c. */

​    uint32_t *pagedir;                  /* Page directory. */

\#endif

 

​    /* Owned by thread.c. */

​    unsigned magic;                     /* Detects stack overflow. */

  };

**tid: 스레드를 구분하는 고유의 id를 저장하는 영역**

**status: 스레드의 현재상태를 저장하는 영역 위의 1)에서 자세하게 설명함.**

**Name: 스레드의 이름을 저장하는 영역. 주로 디버깅 메시지를 확인할 때 사용됨.**

**Stack: 스레드가 사용하는 sp(스택포인터)를 저장하는 영역이다.**

**Priority: 스레드의 우선순위를 저장하는 영역. 자세한 내용은 2)에서 설명함**

**Elem: 스레드 구조체 사이에서 리스트 구성을 위해 이전 스레드 구조체와 다음 스레드 구제체의 포인터를 저장하는 영역이다.**

**Magic: magic number는 스레드 정보와 stack영역 사이에 위치한다. Stack overflow가 발생할 경우, magic number가 변경되기 때문에 에러를 검출하는데 사용된다.**

 

**스레드 구조체의 모습은 다음과 같다.**

4 kB +---------------------------------+

​             |          kernel stack            |

​             |                |                |

​             |                |                |

​             |                V                |

​             |         grows downward        |

​             |                                 |

​             |                                 |

​             |                                 |

​             |                                 |

​             |                                 |

​             |                                 |

​             |                                 |

​             |                                 |

​             +---------------------------------+

​             |              magic             |

​             |                :                |

​             |                :                |

​             |              name              |

​             |              status             |

​        0 kB +---------------------------------+

 

**4)**   **Palloc (palloc.h에 저장된 페이지 관련 구조체 플래그)**

 

/* How to allocate pages. */

enum palloc_flags **//flag****를 비트단위로 할당함**

  {

​    PAL_ASSERT = 001,             **//****페이지 할당을 실패한 경우**

​    PAL_ZERO = 002,              **//****페이지가 0인 경우**

​    PAL_USER = 004              **//user****의 페이지인 경우**

  };

 

**5)**   **Pool(user풀과 kernel풀의 자료구조)**

 

struct pool

  {

​    struct lock lock;                         **//****상호 배제를 위한 lock**

​    struct bitmap *used_map;               **//****사용 중이지 않은 풀의 맵**

​    uint8_t *base;                         **//pool****을 가리키는 포인터**

  };

 

**6)**   **Descriptor( 각 사이즈의 블록을 담당하는 dicriptor)**

 

struct desc

  {

​    size_t block_size;               **//****블록의 크기를 나타냄**

​    size_t blocks_per_arena;        **//****새 메모리의 페이지인 아레나에 있는 블록의 개수를 나타냄**

​    struct list free_list;               **//****빈 블록의 리스트를 나타냄**

​    struct lock lock;                **//****락**

  };

 

\#define ARENA_MAGIC 0x9a548eed **//****아레나가 넘치는 것을 막기 위한 MAGIC**

 

/* Arena. */

struct arena 

  {

​    unsigned magic;             **//****항상 아레나의 매직을 나타냄**

​    struct desc *desc;             **//****새로운 descripor를 할당함**

​    size_t free_cnt;                **//****새로 만든 블록을 빈 블록으로 초기화**

  };

 

/* Free block. */

struct block 

  {

​    struct list_elem free_elem;        **//****내용을 비움**

  };

 

/* Our set of descriptors. */

static struct desc descs[10];        **//****디스크립터**

static size_t desc_cnt;              **//****디스크립터의 개수**

 

static struct arena *block_to_arena (struct block *);     **//****아레나의 포인터**

static struct block *arena_to_block (struct arena *, size_t idx);   

**//block형 포인터인 arena_to_block을 만듦 인자로 아레나 포인터와 사이즈를 전달**

 

**7)**   **Paging (가상 주소공간이 자료구조를 통해 물리주소가 됨)**

 

31                  22 21                  12 11                   0

   +----------------------+----------------------+----------------------+

   | Page Directory Index |   Page Table Index   |    Page Offset       |

   +----------------------+----------------------+----------------------+

 

PDEs and PTEs share a common format:

 

   31                                 12 11                     0

   +------------------------------------+------------------------+

   |         Physical Address           |         Flags          |

   +------------------------------------+------------------------+

 

 

 

**8)**   **Intr_init( 인터럽트 초기화)**

 

enum intr_level 

  {

​    INTR_OFF,             **//****인터럽트 불가**

​    INTR_ON               **//****인터럽트 가능**

  };

 

struct intr_frame

  {

​           **//intr_entry****로 intr_stubs.S에 push 되는 레지스터들**

​    uint32_t edi;               **//edi****저장**        

​    uint32_t esi;               **//esi****저장**

​    uint32_t ebp;              **//ebp****저장**

​    uint32_t esp_dummy;      **//****사용되지 않음**

​    uint32_t ebx;              **//ebx****저장**

​    uint32_t edx;              **//edx****저장**

​    uint32_t ecx;              **//ecx****저장**

​    uint32_t eax;              **//eax****저장**

​    uint16_t gs, :16;           **//GS** **세그먼트 레지스터 저장**

​    uint16_t fs, :16;           **//FS** **세그먼트 레지스터 저장**         

​    uint16_t es, :16;           **//EX****세그먼트 레지스터 저장** 

​    uint16_t ds, :16;           **//DX****세그먼트 레지스터 저장**

 

​    **//intrNN_stub****로 intr_stubs.S에 저장됨**

​    uint32_t vec_no;            **//****인터럽트 벡터 번호**

 

​    uint32_t error_code;        **//****에러 코드**

 

​    void *frame_pointer;        **//frame** **포인터인 EBP저장**

 

​           **//cpu****에 의해 저장됨,인터럽트를 받은 스레드의 레지스터 값을 저장함**

void (*eip) (void);         **//****다음에 실행할 명령어**

​    uint16_t cs, :16;           **//ip****를 위한 코드 세그먼트**

​    uint32_t eflags;            **//cpu** **플래그를 저장**

​    void *esp;                 **//****스택 포인터 저장**

​    uint16_t ss, :16;           **//esp****의 데이터 세그먼트**

  };

 

\#define INTR_CNT 256                  **//** **인터럽트는 최대 256개 생성 가능**

 

/* The Interrupt Descriptor Table (IDT).  The format is fixed by

   the CPU.  See [IA32-v3a] sections 5.10 "Interrupt Descriptor

   Table (IDT)", 5.11 "IDT Descriptors", 5.12.1.2 "Flag Usage By

   Exception- or Interrupt-Handler Procedure". */

static uint64_t idt[INTR_CNT];         **//****인터럽트 디스크립터 테이블을 만듦**

 

 

 

 

 

 

**9)**   **Switch_threads (두 스레드를 교환)**

 

struct switch_threads_frame 

  {

​    uint32_t edi;               **//0: edi**

​    uint32_t esi;               **//4: esi**

​    uint32_t ebp;              **//8:ebp**

​    uint32_t ebx;              **//12:ebx**

​    void (*eip) (void);         **//16:** **복귀주소**

​    struct thread *cur;         **//20:switch_thread****의 cur**

​    struct thread *next;        **//24: switch_thread****의 next**

  };

 

/* Offsets used by switch.S. */

\#define SWITCH_CUR      20       **//20** **오프셋은 항상 cur의 위치**

\#define SWITCH_NEXT     24       **//24** **오프셋은 항상 next의 위치**

 

 

 

**IV.**          **함수 설명**

 

**1)**   **bss_init(bss** **영역을 초기화함)**

 

bss_init (void) 

{

  extern char _start_bss, _end_bss; **//bss****의 시작값과 끝값 kernel.lds.S에 있는 값**

memset (&_start_bss, 0, &_end_bss - &_start_bss); 

**//시작주소부터 끝주소에서 시작주소를 뺀 값만큼 0으로 초기화한다.** 

}

**2)**   **read_command_line(****입력된 것을 문자열로 바꿔서 저장함)**

 

read_command_line (void) 

{

  static char *argv[LOADER_ARGS_LEN / 2 + 1];

  char *p, *end;

  int argc;

  int i;

 

  argc = *(uint32_t *) ptov (LOADER_ARG_CNT);       **//argc****에 입력된 문자열 개수 저장**

  p = ptov (LOADER_ARGS);

  end = p + LOADER_ARGS_LEN;

  for (i = 0; i < argc; i++) 

​    {

​      if (p >= end)

​        PANIC ("command line arguments overflow");

 

​      argv[i] = p;

​      p += strnlen (p, end - p) + 1;

​    }

  argv[argc] = NULL;       

 

  /* Print kernel command line. */

  printf ("Kernel command line:");

  for (i = 0; i < argc; i++)

​    if (strchr (argv[i], ' ') == NULL)

​      printf (" %s", argv[i]);

​    else

​      printf (" '%s'", argv[i]);

  printf ("\n");

 

  return argv;      **//****문자열을 argv에 저장하여 반환함**

}

 

**3)**   **parse_option(argv****에 저장된 문자열을 토큰으로 파싱함)**

 

**//****각각의 옵션 중에 해당하는 것이 있으면 해당하는 함수를 실행함.**

parse_options (char **argv) 

{

  for (; *argv != NULL && **argv == '-'; argv++)

​    {

​      char *save_ptr;

​      char *name = strtok_r (*argv, "=", &save_ptr);

​      char *value = strtok_r (NULL, "", &save_ptr);

​      

​      if (!strcmp (name, "-h"))

​        usage ();

​      else if (!strcmp (name, "-q"))

​        shutdown_configure (SHUTDOWN_POWER_OFF);

​      else if (!strcmp (name, "-r"))

​        shutdown_configure (SHUTDOWN_REBOOT);

\#ifdef FILESYS

​      else if (!strcmp (name, "-f"))

​        format_filesys = true;

​      else if (!strcmp (name, "-filesys"))

​        filesys_bdev_name = value;

​      else if (!strcmp (name, "-scratch"))

​        scratch_bdev_name = value;

\#ifdef VM

​      else if (!strcmp (name, "-swap"))

​        swap_bdev_name = value;

\#endif

\#endif

​      else if (!strcmp (name, "-rs"))

​        random_init (atoi (value));

​      else if (!strcmp (name, "-mlfqs"))

​        thread_mlfqs = true;

\#ifdef USERPROG

​      else if (!strcmp (name, "-ul"))

​        user_page_limit = atoi (value);

\#endif

​      else

​        PANIC ("unknown option `%s' (use -h for help)", name);

​    }

 

  /* Initialize the random number generator based on the system

​     time.  This has no effect if an "-rs" option was specified.

 

​     When running under Bochs, this is not enough by itself to

​     get a good seed value, because the pintos script sets the

​     initial time to a predictable value, not to the local time,

​     for reproducibility.  To fix this, give the "-r" option to

​     the pintos script to request real-time execution. */

  random_init (rtc_get_time ());

  

  return argv;                  

}

**4)**   **thread_init (thread.c****에 정의된 함수, 최초의 스레드를 만들고 큐를 초기화함)**

 

thread_init (void) 

{

  ASSERT (intr_get_level () == INTR_OFF);                **//****참이 아니면 프로그램 중단** 

 

  lock_init (&tid_lock);       **//****동기화를 위해 사용된다. 한번에 한 스레드만 tid에 접근하게 함**

  list_init (&ready_list);       **//****레디큐를 초기화함**

  list_init (&all_list);           **//****모든 큐를 초기화함**

 

  /* Set up a thread structure for the running thread. */

  initial_thread = running_thread ();    **//intial_thread****를 running_thread로 함**

init_thread (initial_thread, "main", PRI_DEFAULT);       

**//intial_thread의 이름을 main, 우선순위는 default인 31로 함.**

  initial_thread->status = THREAD_RUNNING; **//initial_thread****의 상태는 running으로 함**

  initial_thread->tid = allocate_tid ();  **//****새로운 tid를 initial_thread에 부여함**

}

 

**5)**   **palloc_init(페이지 공간을 초기화하는 함수)**

 

palloc_init (size_t user_page_limit)

{

  /* Free memory starts at 1 MB and runs to the end of RAM. */

uint8_t *free_start = ptov (1024 * 1024);                                                 (ㄱ)

uint8_t *free_end = ptov (init_ram_pages * PGSIZE);                        (ㄴ)

  size_t free_pages = (free_end - free_start) / PGSIZE;                                 (ㄷ)

  size_t user_pages = free_pages / 2;                                                      (ㄹ)

  size_t kernel_pages;                                                                          (ㅁ)

  if (user_pages > user_page_limit)                                                 (ㅂ)

​    user_pages = user_page_limit;                                                 (ㅅ)

  kernel_pages = free_pages - user_pages;                                     (ㅇ)

 

  /* Give half of memory to kernel, half to user. */

  init_pool (&kernel_pool, free_start, kernel_pages, "kernel pool");                      (ㅈ)

  init_pool (&user_pool, free_start + kernel_pages * PGSIZE,                 (ㅊ)

​             user_pages, "user pool");

}

**(ㄱ)**  **uint8_t는 자료구조 5)에 설명한 pool의 시작주소를 의미한다. Pool의 시작주소 free_start에 1MB 크기의 빈 공간을 할당한다.**

**(ㄴ)**  **초기 설정한 크기만큼을 곱해서 pool의 끝주소를 구하고 free_end에 pool의 끝주소를 저장한다.**

**(ㄷ)**  **풀의 끝 주소에서 시작주소를 빼고 그것을 페이지 하나의 크기로 나눠서 개수를 구하고 빈 페이지인 free_pages에 저장한다.**

**(ㄹ)**  **빈 페이지의 반을 user 페이지의 크기로 하고**

**(ㅁ)**  **커널페이지를 할당한다**

**(ㅂ)**  **유저페이지가 유저페이지 제한보다 크면**

**(ㅅ)**  **유저페이지를 제한으로 맞추고**

**(ㅇ)**  **커널페이지는 전체 풀에서 유저를 제외한 나머지로 저장한다.**

**(ㅈ)**  **커널 풀의 주소, 커널의 시작을 가리키는 포인터, 커널 페이지의 개수, 커널 풀의 이름을 init_pool함수에 넣어 커널 풀을 만든다.**

**(ㅊ)**  **유저 풀의 주소,  유저풀의 시작을 가리키는 포인터, 유저 페이지의 개수, 유저 풀의 이름을 init_pool함수에 넣어 유저 풀을 생성한다.**

Palloc_init 함수가 동작한 후의 memory pool의 구조는 다음과 같다

 

4GB-------------------------------+ free_end== Ram_page*PGSIZE

​             |            user pool            |

​             |---------------------------|

​             |          kernel pool             |

​             |---------------------------|free_start== ptov (1024 * 1024)

​             |              .bss               |

​             |---------------------------|

​             |             .data               |

​             |---------------------------|

​             |              .rodata            |

​             |---------------------------|

​             |              .text               |

​             |---------------------------|

​             |              1MB                |

​        3GB +----------------------------+

 

**6)**   **Malloc_init(****동적 할당받는 메모리를 초기화하는 함수)**

 

 

malloc_init (void)   **//malloc****을 초기화**

{

  size_t block_size;

 

  for (block_size = 16; block_size < PGSIZE / 2; block_size *= 2)                    (ㄱ)

​    {

​      struct desc *d = &descs[desc_cnt++];                                                        (ㄴ)

​      ASSERT (desc_cnt <= sizeof descs / sizeof *descs);                                 (ㄷ)

​      d->block_size = block_size;                                                      		    (ㄹ)

​      d->blocks_per_arena = (PGSIZE - sizeof (struct arena)) / block_size;    (ㅁ)

​      list_init (&d->free_list);                                                                      	   (ㅂ)

​      lock_init (&d->lock);                                                            		         (ㅅ)

​    }

}

 

 

**(ㄱ)** **블록사이즈를 16으로 초기화, 블록사이즈가 페이지사이즈/2보다 작으면 블록사이즈를 2배씩 증가**

**(ㄴ)** **디스크립터 포인터인 d에 디스크립터의 개수를 인덱스로 디스크립터의 주소값을 저장함**

**(ㄷ)** **디스크립터의 개수가 부족하면 프로그램 중단**

**(ㄹ)** **디스크립터의 블록사이즈에 블록사이즈를 저장**

**(ㅁ)** **디스크립터의 block_per_arena에 페이지크기에서 아레나크기를 뺴고 블로사이즈로 나눈것을 저장**

**(ㅂ)** **디스크립터의 빈 블록을 나타내는 주소값을 list_init 함수에 인자로 전달**

**(ㅅ)** **디스크립터의 lock을 lock_init으로 전달하여 초기화함**

 

 

 

 

 

**7)**   **Paging_init(페이지를 초기화하는 함수)**

 

paging_init (void)

{

  uint32_t *pd, *pt;                                **//****페이지 포인터 pd와 pt**

  size_t page;                                       **//****페이지의 크기**

  extern char _start, _end_kernel_text;

 

  pd = init_page_dir = palloc_get_page (PAL_ASSERT | PAL_ZERO);

  pt = NULL;

  for (page = 0; page < init_ram_pages; page++)        **//****페이지가 0부터 할당한 페이지만큼**

​    {

​      uintptr_t paddr = page * PGSIZE;        **//paddr****에 page\*페이지 사이즈를 저장**

​      char *vaddr = ptov (paddr);              **//char** **포인터형 vaddr에 ptov(paddr)를 저장**

​      size_t pde_idx = pd_no (vaddr);          **//pd****번호를 pde_idx에 저장**

​      size_t pte_idx = pt_no (vaddr);           **//pt****번호를 pre_idx에 저장**

​      bool in_kernel_text = &_start <= vaddr && vaddr < &_end_kernel_text;

 

​      if (pd[pde_idx] == 0)

​        {

​          pt = palloc_get_page (PAL_ASSERT | PAL_ZERO);

​          pd[pde_idx] = pde_create (pt);

​        }

 

​      pt[pte_idx] = pte_create_kernel (vaddr, !in_kernel_text);

​    }

  asm volatile ("movl %0, %%cr3" : : "r" (vtop (init_page_dir)));

}

 

 

 

 

 

 

 

 

 

 

**8)**   **Intr_init(IDT****를 초기화하여 각 인터럽트를 저장함)**

 

/* Initializes the interrupt system. */

void

intr_init (void)

{

  uint64_t idtr_operand;

  int i;

 

pic_init (); **//****인터럽트 컨트롤러를 초기화함**

 

  /* Initialize IDT. */

  for (i = 0; i < INTR_CNT; i++)

​    idt[i] = make_intr_gate (intr_stubs[i], 0);  **//****각 번호의 intr_stub를 idt에 저장함**

 

  /* Load IDT register.

​     See [IA32-v2a] "LIDT" and [IA32-v3a] 5.10 "Interrupt

​     Descriptor Table (IDT)". */

  idtr_operand = make_idtr_operand (sizeof idt - 1, idt);

  asm volatile ("lidt %0" : : "m" (idtr_operand));

 

  /* Initialize intr_names. */

  for (i = 0; i < INTR_CNT; i++)                   **//****각 인터럽트를 초기화함**

  intr_names[i] = "unknown";

  intr_names[0] = "#DE Divide Error";

  intr_names[1] = "#DB Debug Exception";

  intr_names[2] = "NMI Interrupt";

  intr_names[3] = "#BP Breakpoint Exception";

  intr_names[4] = "#OF Overflow Exception";

  intr_names[5] = "#BR BOUND Range Exceeded Exception";

  intr_names[6] = "#UD Invalid Opcode Exception";

  intr_names[7] = "#NM Device Not Available Exception";

  intr_names[8] = "#DF Double Fault Exception";

  intr_names[9] = "Coprocessor Segment Overrun";

  intr_names[10] = "#TS Invalid TSS Exception";

  intr_names[11] = "#NP Segment Not Present";

  intr_names[12] = "#SS Stack Fault Exception";

  intr_names[13] = "#GP General Protection Exception";

  intr_names[14] = "#PF Page-Fault Exception";

  intr_names[16] = "#MF x87 FPU Floating-Point Error";

  intr_names[17] = "#AC Alignment Check Exception";

  intr_names[18] = "#MC Machine-Check Exception";

  intr_names[19] = "#XF SIMD Floating-Point Exception";

}

 

 

 

 

 

 

 

 

**//inte-stubs.S****에 있는 어셈블리어로 작성된 intr_entry, intr_exit, intr_handler**

 

intr_entry:

​           **//caller****의 레지스터를 현재 실행중인 스레드의 스택에 저장함**

​           pushl %ds

​           pushl %es

​           pushl %fs

​           pushl %gs

​           pushal

​        

​           /* Set up kernel environment. */

​           cld                               /* String instructions go upward. */

​           mov $SEL_KDSEG, %eax  /* Initialize segment registers. */

​           mov %eax, %ds

​           mov %eax, %es

​           leal 56(%esp), %ebp         /* Set up frame pointer. */

 

​           **//intr_handler****를 call함**

​           pushl %esp

.globl intr_handler

​           call intr_handler

​           addl $4, %esp

 

**//****호출된 intr_handler**

 

intr_handler (struct intr_frame *frame) 

{

  bool external;

  intr_handler_func *handler;

 

external = frame->vec_no >= 0x20 && frame->vec_no < 0x30;           **//****외부 인터럽트**

  if (external) 

​    {

​      ASSERT (intr_get_level () == INTR_OFF);          **//****인터럽트가 꺼져있는지 확인**

​      ASSERT (!intr_context ());

 

​      in_external_intr = true;

​      yield_on_return = false;                    **//** **반환을 하지않음**

​    }

 

  /* Invoke the interrupt's handler. */

  handler = intr_handlers[frame->vec_no];    **//****벡터번호의 인터럽트 핸들러를 저장**

  if (handler != NULL)

​    handler (frame);

  else if (frame->vec_no == 0x27 || frame->vec_no == 0x2f)

​    {

}

  else

​    unexpected_interrupt (frame);

 

  /* Complete the processing of an external interrupt. */

  if (external)                                        **//****외부 인터럽트인 경우 즉, 타이머**

​    {

​      ASSERT (intr_get_level () == INTR_OFF);          **//****인터럽트를 받지 않고**

​      ASSERT (intr_context ());

 

​      in_external_intr = false;                                **//in_external_intr****를 false로 하고**

​      pic_end_of_interrupt (frame->vec_no); 

 

​      if (yield_on_return)                          **//****반환이 true이면**

​        thread_yield ();                                       **//running****에서 ready로 반환함**

​    }

}

 

intr_exit:

​          **//caller의 레지스터를 가시 저장함**

​           popal

​           popl %gs

​           popl %fs

​           popl %es

​           popl %ds

 

​        /* Discard `struct intr_frame' vec_no, error_code,

​           frame_pointer members. */

​           addl $12, %esp

 

​        **//interrupt****에서 복귀하여 caller에게 감**

​           iret

 

 

 

 

**//****인터럽트 발생 후 처리 순서를 정리하자면**

 

**ㄱ.**  **cpu****신호가 발생하면 현재 실행중인 스레드의 스택에 ss, esp,eflag,eip를 저장함**

**ㄴ.**  **발생한 신호의 벡터번호를 확인하여 intrNN_stub에서 어떤 장치의 인터럽트인지 확인하고 ebp, error code, vector.no를 스택에 저장함**

**ㄷ.**  **Intr_entry****로 가서 현재 실행중인 레지스터값을 저장함. Ds, es, fs, qs, eax, ecx, edx, ebx, esp, ebp, esi, edi를 저장함. 그리고 intr_handler를 호출함**

**ㄹ.**  **Intr_handler****는 스택에 제공된 vecter.no를 통해 언터럽트 처리함수를 실행한다. 그리고 return하여 entry로 돌아가면 순차적으로 intr_exit이 실행됨**

**ㅁ.**  **Intr_exit****에서 저장했던 레지스터값을 복원하고 caller로 복귀함.**

 

 

 

 

 

 

 

 

 

 

 

 

**9)**   **Timer_init (****타이머 초기화)**

 

timer_init (void) 

{

  pit_configure_channel (0, 2, TIMER_FREQ);

  intr_register_ext (0x20, timer_interrupt, "8254 Timer");            **//****타이머의 인터럽트 번호는 0x20**

}

 

**10)**  **Kdb_init (****키보드 초기화)**

 

kbd_init (void) 

{

intr_register_ext (0x21, keyboard_interrupt, "8042 Keyboard");  

**//키보드의 인터럽트 번호는 0x21**

}

 

**11)** **Input_init (입력을 초기화)**

 

input_init (void) 

{

  intq_init (&buffer);          **//****입력 버퍼를 초기화함**

}

 

 

**12)** **Thread_start (idle****스레드를 만들고 스케줄링을 가능하도록 함)**

thread_start (void) 

{

  struct semaphore idle_started;

  sema_init (&idle_started, 0);

  thread_create ("idle", PRI_MIN, idle, &idle_started);     **//idle** **스레드를 만듦**

 

  /* Start preemptive thread scheduling. */

  intr_enable ();                                      **//****선점 스케줄링 하기 위해 intr_enalbe을 함**   

 

  /* Wait for the idle thread to initialize idle_thread. */

  sema_down (&idle_started);

}

 

**//idle 스레드는 아무 스레드도 실행하지 않을 때 실행됨**

idle (void *idle_started_ UNUSED) {

  struct semaphore *idle_started = idle_started_;

  idle_thread = thread_current ();

  sema_up (idle_started);

 

  for (;;) 

​    {

​      intr_disable ();                    **//****다른 스레드가 돌도록 block함**

​      thread_block ();

 

​      asm volatile ("sti; hlt" : : : "memory");

​    }

}

**//thread_create (새로운 스레드를 만드는 함수**

 

thread_create (const char *name, int priority,

​               thread_func *function, void *aux) 

{

  struct thread *t;

  struct kernel_thread_frame *kf;

  struct switch_entry_frame *ef;

  struct switch_threads_frame *sf;

  tid_t tid;

  enum intr_level old_level;

 

  ASSERT (function != NULL);

 

  /* Allocate thread. */

  t = palloc_get_page (PAL_ZERO); **//tcb****페이지를 할당함**

  if (t == NULL)

​    return TID_ERROR;

 

  /* Initialize thread. */

  init_thread (t, name, priority);                   **//****이름과 우선순위 부여**

  tid = t->tid = allocate_tid ();

 

old_level = intr_disable ();               **//****인터럽트가 불가능하게 함**

 

  /* Stack frame for kernel_thread(). */        **//****이후 동작은 스택 초기화**

  kf = alloc_frame (t, sizeof *kf);

  kf->eip = NULL;

  kf->function = function;

  kf->aux = aux;

 

  /* Stack frame for switch_entry(). */

  ef = alloc_frame (t, sizeof *ef);

  ef->eip = (void (*) (void)) kernel_thread;

 

  /* Stack frame for switch_threads(). */

  sf = alloc_frame (t, sizeof *sf);

  sf->eip = switch_entry;

  sf->ebp = 0;

 

  intr_set_level (old_level);

 

  /* Add to run queue. */

  thread_unblock (t);

 

  return tid;

}

**//** **스택에 저장되는 값은 마치 새로 생긴 스레드가 실행되고 있던 스레드 처럼 보이게 한다. 따라서 이후 schedule() 함수에서 entry의 switch가 일어날 때 문제가 발생하지 않는다.**

 

 

 

**//thread_ticks(ticks****와 time slice를 비교하여 같으면 running에서 ready로 감**

 

thread_tick (void) 

{

  struct thread *t = thread_current ();           **//****현재 스레드를 저장**

 

  /* Update statistics. */

  if (t == idle_thread)                                       

​    idle_ticks++;                                    **//idle** **이면 idle tick 증가**

\#ifdef USERPROG

  else if (t->pagedir != NULL)

​    user_ticks++;                        **//****유저이면 유저tick 증가**

\#endif

  else

​    kernel_ticks++;                                 **//****커널이면 커널tick 증가**

 

  /* Enforce preemption. */

  if (++thread_ticks >= TIME_SLICE)

​    intr_yield_on_return ();              **//time slice****와 같으면 반환**

}

 

 

**//thread_yeild**

 

thread_yield (void) 

{

  struct thread *cur = thread_current ();        **//****현재 스레드를 cur에 저장**

  enum intr_level old_level;

  

  ASSERT (!intr_context ());                      **//intr_context****이면 프로그램 종료**

 

  old_level = intr_disable ();            **//****인터럽트를 받지않음**

  if (cur != idle_thread) 

​    list_push_back (&ready_list, &cur->elem); **//cur****를 ready큐에 저장**

  cur->status = THREAD_READY;                          **//****상태를 ready큐로 바꿈**

  schedule ();                                                   **//schedule****함수 호출**

  intr_set_level (old_level);                         **//****인터럽트가 가능하게 함**

}          

 

 

**//thread_block**

 

thread_block (void) 

{

  ASSERT (!intr_context ());                      **//intr_context****이면 프로그램 종료**

  ASSERT (intr_get_level () == INTR_OFF);**//****인터럽트가 꺼져있지 않으면 프로그램 종료함**

 

  thread_current ()->status = THREAD_BLOCKED;      **//****현재 상태를 블록으로 하고** 

  schedule ();                                                   **//shedule****함수 호출**

}

 

 

**//thread_exit**

 

thread_exit (void) 

{

  ASSERT (!intr_context ());                      **//intr_context****이면 프로그램 종료**

 

\#ifdef USERPROG

  process_exit ();

\#endif

 

  /* Remove thread from all threads list, set our status to dying,

​     and schedule another process.  That process will destroy us

​     when it calls thread_schedule_tail(). */

  intr_disable ();                                      **//****인터럽트가 불가능하게 하고**

  list_remove (&thread_current()->allelem);     **//****스레드를 큐에서 삭제함**

  thread_current ()->status = THREAD_DYING;           **//****상태를 dying으로 함**

  schedule ();                                        **//****다음 스레드의 실행을 위해 schedule 호출**

  NOT_REACHED ();                               **//****절대 닿지 않는 영역** 

}

 

 

**//schedule (****레디큐에 있는 다음 스레드를 실행하기 위한 함수)**

 

schedule (void) 

{

  struct thread *cur = running_thread ();                    **//****현재 실행중인 스레드 cur**

  struct thread *next = next_thread_to_run (); **//****다음에 실행할 스레드 next**

  struct thread *prev = NULL;                    **//****스케줄 함수 종료할 cur를 prev에 넣어 리턴**

 

  ASSERT (intr_get_level () == INTR_OFF);                **//****인터럽트를 받지 않음**

  ASSERT (cur->status != THREAD_RUNNING);         **//cur****의 상태가 running이 아니어야 함**

  ASSERT (is_thread (next));                                 **//****다음에 실행할 스레드가 있어야 함**

 

  if (cur != next)

​    prev = switch_threads (cur, next);          **//running****을 cur에서 next로 바꾸고 cur를 리턴** 

  thread_schedule_tail (prev);                     **//cur****였던 prev를 리턴함**

}

 

**//switch_threads (cur****와 next를 받아 next를 running하게하고 cur를 prev에 넣어 돌려줌)**

 

switch_threads:

​           **//caller****의 레지스터 상태를 저장함**

​           pushl %ebx

​           pushl %ebp

​           pushl %esi

​           pushl %edi

 

​           \# Get offsetof (struct thread, stack).

.globl thread_stack_ofs

​           mov thread_stack_ofs, %edx

 

​           \# Save current stack pointer to old thread's stack, if any.

​           movl SWITCH_CUR(%esp), %eax     **//stack****의 top인 esp를 eax에 저장**

​           movl %esp, (%eax,%edx,1)           **//****스택의 top인 esp는 stack의 top을 가리키게 함**

 

​           \# Restore stack pointer from new thread's stack.

​           movl SWITCH_NEXT(%esp), %ecx   **//next****의 stack의 top을 가키리는 것을 ecx에 저장**

​           movl (%ecx,%edx,1), %esp           **//offset****의 위치를 stack의 top이 가리키게 함**

 

​                                                         **//caller****의 레지스터 상태를 pop함**

​           popl %edi

​           popl %esi

​           popl %ebp

​           popl %ebx

​        ret

.endfunc

 

**//schedule_tail** **스케줄을 마무리하는 함수**

 

thread_schedule_tail (struct thread *prev)

{

  struct thread *cur = running_thread ();

  

  ASSERT (intr_get_level () == INTR_OFF);

 

  /* Mark us as running. */

  cur->status = THREAD_RUNNING; 

 

  /* Start new time slice. */

  thread_ticks = 0;

 

\#ifdef USERPROG

  /* Activate the new address space. */

  process_activate ();

\#endif

 

  

  if (prev != NULL && prev->status == THREAD_DYING && prev != initial_thread) 

​    {

​      ASSERT (prev != cur);

​      palloc_free_page (prev);        **//****상태가 dying이면 free로 메모리를 free함**

​    }

}

 

 

 

 

 

 

 

 

 

 

 

**//switch_entry**

 

switch_entry:

​           

​           addl $8, %esp     **//switch_threads****의 요소인 cur와 next를 지우는 효과**

 

​           \# Call thread_schedule_tail(prev).

​           pushl %eax                    **//schedule_tail****의 파라미터**

.globl thread_schedule_tail

​           call thread_schedule_tail

​           addl $4, %esp                **//****파라미터를 제거함**

 

​           \# Start thread proper.

​           ret

.endfunc

 

 

**13)** **Serial_init_queue(** **인터럽트에 의한 io를 위해 시리얼 큐를 초기화함**

 

serial_init_queue (void) 

{

  enum intr_level old_level;

 

  if (mode == UNINIT)

​    init_poll ();

  ASSERT (mode == POLL);

 

  intr_register_ext (0x20 + 4, serial_interrupt, "serial");

  mode = QUEUE;

  old_level = intr_disable ();

  write_ier ();

  intr_set_level (old_level);

}

 

**14)** **Timer_calibrate (****타이머의  ticks을 계산하는 함수)**

 

 

/* Calibrates loops_per_tick, used to implement brief delays. */

void

timer_calibrate (void) 

{

  unsigned high_bit, test_bit;

 

  ASSERT (intr_get_level () == INTR_ON);

  printf ("Calibrating timer...  ");

 

  /* Approximate loops_per_tick as the largest power-of-two

​     still less than one timer tick. */

  loops_per_tick = 1u << 10;

  while (!too_many_loops (loops_per_tick << 1)) 

​    {

​      loops_per_tick <<= 1;

​      ASSERT (loops_per_tick != 0);

​    }

 

  /* Refine the next 8 bits of loops_per_tick. */

  high_bit = loops_per_tick;

  for (test_bit = high_bit >> 1; test_bit != high_bit >> 10; test_bit >>= 1)

​    if (!too_many_loops (high_bit | test_bit))

​      loops_per_tick |= test_bit;

 

  printf ("%'"PRIu64" loops/s.\n", (uint64_t) loops_per_tick * TIMER_FREQ);

}

 

**15)** **Run_action (****응용프로그램을 실행하는 함수 이번 과제에서는 alarm-multiple을 실행한다)**

 

run_actions (char **argv)   

{

  /* An action. */

  struct action 

​    {

​      char *name;                       /* Action name. */

​      int argc;                         /* # of args, including action name. */

​      void (*function) (char **argv);   /* Function to execute action. */

​    };

 

 