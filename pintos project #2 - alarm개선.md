

**목차**

**I.**         **문제 정의**

**II.**       **해결 방안**

**1.**   **도식화**

**2.**   **Timer_sleep** **개선**

**3.**   **Timer_interrupt** **개선**

**III.**     **구현**

**1.** **함수와 자료구조**

**2. Timer_sleep****함수**

**3.Thread_check****함수**

**4. Thread_compare****함수**

**5. My_init** **함수**

**6. Timer_interrupt** **함수**

**7. Run_action** **함수**

 

**IV.**     **테스트**

**1.**   **Alarm-single**

**2.**   **Alarm-multiple**

**3.**   **Alarm-priority**

**4.**   **Alarm-sumultaneous**

**5.**   **Alarm-zero**

**6.**   **Alarm-negative**

​                           

 

 

**I.**        **문제 정의**

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image002.jpg)

Timer-sleep 함수의 모습은 위와 같다. 현재 시간을 읽어 start에 저장하고, timer-sleep함수가 실행될 때는 인터럽트가 꺼져 있어야 한다. 

현재의 구현은 while문 안에서 ticks 틱이 경과할 때까지 thread_yeild를 반복 호출한다. 이는 busy_waiting 방법으로 cpu cycle의 소모가 크다. 따라서 busy_waiting 되는 부분을 non-busy-waiting으로 변경하여 수행함으로 성능을 개선한다.

 

**II.**      **해결 방안**

 

\1.    Timer_sleep 함수를 호출한 스레드들이 대기할 수 있는 리스트를 만들고 현재 시각을 기준으로 ticks 시간이 경과할 때까지 block시킨다. 시간이 경과하면 해당 스레드를 리스트에서 꺼내고 unblock한다. 

 

가) 기존 방식

![EMB00000f44aa57](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image004.jpg)

 

 

 

 

 

 

 

 

 

 

 

 

 

 

나) 개선된 방식

![EMB00000f44aa58](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image006.jpg)

 

**Timer_sleep****함수 개선**

\-     스레드를 리스트에 넣고 thread_block 함수를 호출하여 해당 스레드를 block시킨다.

 

 

**Timer_interrupt** **함수 개선**

\-     인터럽트 과정에서 리스트 중 시간이 만료된 것이 있는지 검사하고 완료된 스레드를 thread_unblock 함수를 통해 깨운다. 

 

 

 

 

 

**III.**    **구현** 

\1.   함수와 자료구조

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image008.jpg)

\- Thread_compare를 통해 시간이 만료된 스레드를 unblock한다.

\- Thread_compare가 true일때만 검사하기 위해 bool타입의 변수 true선언

\- Waiting queue에 넣을 때 만료시간이 가장 작은 것이 앞에 있도록 하는 함수 thread_check

\- 구조체 자료형 alarm_list를 초기화하는 my_init함수

\- waiting queue를 위한 alarm_list

 

구조체 alarm은 아래와 같다.

struct alarm

{

​           int64_t deadLine;             		//알람 만료시간

​           struct thread * myThread;              //알람 요청한 스레드

​           struct list_elem elem;                    //알람 리스트 연결 필드

};

**2.**  **Timer_sleep** **함수**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image010.jpg)

\- 현재 시점의 tick값과 주어진 ticks를 더하여 알람 만료시간을 구한다.

\- malloc으로 공간을 할당 받아 현재 스레드와 time값을 저장한다.

\- 현재 인터럽트의 상태를 알려주는 열거형 old_level;

\- intr_disable함수는 인터럽트를 끄고 이전 상태의 intrrupt를 반환한다.

-list_insert_ordered함수는 정해진 순서대로 리스트에 저장한다.

-running중인 스레드를 block 상태로 바꾸고 unblock 할때까지 실행하지 않는다.

-인터럽트를 키고 이전 상태의 인터럽트를 반환한다.

**3. thead_check** **함수**

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image012.jpg)

\- 리스트에 삽입할 때 deadline이 작은 순으로 삽입하기 위한 함수이다.

\- 리스트 속의 struct에 속한 멤버를 찾고 그 멤버의 offset을 빼서 해당 struct의 시작주소를 얻는다.

\- waiting큐에 들어가려고 하는 스레드 값이 waiting큐 안에 있는 값보다 크면 false를 반환함. 

 

**4.thread_compare****함수**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image014.jpg)

\- waiting queue에 만료시간이 가장 작은 스레드와 시간을 비교하고 일정 시간이 지나면 unblock하는 함수

\- turn이 true이고 list사이즈가 0이 아닐 때

\- 구조체 alarm의 포인터 my

\- 현재 인터럽트의 상태를 나타내는 열거형 old_level

\- 만료시간이 가장 작은 구조체를 반환하여 그 값이 tick보다 작은지 확인

\- 작으면 waiting 큐에서 꺼내어 unblock하여 레디큐에 넣고, intr를 받기 시작한다.



 

**5. my_init****함수**

**![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image016.jpg)**

\- 리스트를 초기화하는 함수

 

**6. timer_interrupt** **함수**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image018.jpg)

\- tick을 증가하면서 thread_compare를 통해 깨어날 스레드가 있는지 확인한다. 

 

**7. run_actions**

**![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image020.jpg)**

**-** run action에 my_init을 추가하여 초기화한다.

 

 

 

 



 

**IV.**    **테스트**

 

**1.**  **Alarm-single**

**-pass**

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image022.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image024.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image026.jpg)

 

수정 전은 idle 0, 커널 357이다. 수정 후는 idle 250 커널 110으로 커널 tick이 감소하고 idle tick이 증가한 것을 볼 수 있다.

 

 

**2.**  **Alarm-multiple**

**-pass**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image028.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image030.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image032.jpg)

 

수정 전 idle 0, 커널851에서 수정후 idle 550 커널 303이다. 역시 idle이 증가하고 커널이 감소하는 것을 볼 수 있다.

 

 

 



 

**3.**  **Alarm-simultaneous**

**-pass**

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image034.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image036.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image038.jpg)

 

수정전 idle 0 커널 410에서 수정후 idle 250 커널 162로 역시 idle이 증가하고 커널이 감소했다.

 

 

 

 

 

 

 

 

 

 

 

 

 

**4.**  **Alarm-priority**

\-    **Fail(****아직 우선순위를 하지않음)**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image040.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image042.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image044.jpg)

 

수정 전 idle 0, 커널 595 수정후 idle469 커널 125. idle증가 커널 감소

 

 

 

 

**5.**  **Alarm-zero**

**-pass**

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image046.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image048.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image050.jpg)

수정 전 idle 0 커널 35, 수정 후 idle 1 커널 36. idle도 증가하고 커널도 증가했다.  

 

 



**6.**  **Alarm-negative**

**-pass**

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image052.jpg)

 

수정 전)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image054.jpg)

 

수정 후)

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image056.jpg)

수정 전 idle 0 커널 38. 수정 후 idle 1 커널 38. Idle만 1 증가했다. 

 

![img](file:///C:\Users\창용\AppData\Local\Temp\msohtmlclip1\01\clip_image058.jpg)