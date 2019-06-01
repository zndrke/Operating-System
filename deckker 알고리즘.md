deckker 알고리즘

~~~c

boolean flag[2];
int turn;

do{
    flag[i]=true;
    while(flag[j]){
        if(turn=j){
            flag[i]=false;
            while(turn=j)
                ;
            flag[i]=true;
        }
    }
    	/* critical section*/
    turn =j;
    flag[i]=false;
    	/*remainder section*/
}while(true);
~~~



임계구역 문제의 세가지 조건은 Mutual exclusion, progress, bounded waiting 이다. Mutual exclusion은 하나의 프로세스가 critical section을 실행 중일 때 다른 프로세스가 critical section에 진입하지 못하도록 하는 것을 말한다. Progress는 자신이 critical section이 아닌 remainder section에 있으면서 다른 프로세스의 critical section 진입을 막아서는 안되는 것을 말한다. Bounded waiting은 진입 시도가 유한해야 함을 말한다. 한 프로세스가 자신의 임계 구역에 진입하고자 요청을 한 후부터 이 요청이 허용될 때까지 다른 프로세스가 그들의 임계 구역에 진입할 수 있는 횟수가 제한되어야 한다.

 

Flag[i]는 프로세스 i가 임계영역에 들어갈 수 있는지를 나타내고, turn은 누구의 차례인지 나타내는 변수이다. 

 

1)    Mutual exclusion

\-     프로세스 i가 임계영역에 들어가기 위해서는 flag[i]가 true이고, turn이 i여야 한다. 마찬가지로 프로세스 j가 임계영역에 들어가기 위해서는 flag[j]가 true이고, turn이 j여야 한다. Turn의 값은 critical section이 실행된 다음에 변경되기 때문에 하나의 프로세스가 실행 중일 때 다른 프로세스가 임계영역에 진입할 수 없다. 

 

2)    Progress

\-     위의 코드에서 critical section 직후에 turn을 j로 하여 다른 프로세스(j)의 진입이 가능하도록 했다. 따라서 프로세스 i가 임계영역을 지난 후 remainder 영역을 실행할 때는 프로세스 j가 자신의 임계영역을 실행할 수 있다. 

\-      

3)    Bounded waiting

\-     프로세스 i가 임계영역을 지나면 스스로 flag[i]를 false로 만든다. 따라서 프로세스 j는 do 문의 첫 번 째 while의 조건인 flag[i]가 false가 되어 바로 프로세스 j의 임계영역을 실행한다. 즉, 프로세스 i가 임계영역을 지나면서 flag[i]를 false로 하여 최소한 한번은 프로세스 j의 임계영역 진입을 보장하는 것이다.