
![[Pasted image 20230716102853.png]]

- **T****h****e main branches  
      
    **

- master

- 기본적으로 git에서 생성되는 branch.
- 운용 기준

- HEAD부분은 제품으로 나갈만큼 안정화되어 있어야 한다.  
      
    

- develop

- 개발시 이용하는 branch
- 운용 기준

- 최근 개발 현황이 HEAD에 담겨야 한다.
- 다음 release를 위한 기능 추가가 이루어 진다.
- auto build 및 test 대상이 된다.
- 안정화가 끝나면 master 와 merging되고 release tag 번호가 부여된다.

- **Supporting branches** : 수시로 생성과 삭제가 반복되는 branch

- **feature**

- 새로운 기능을 추가할때마다 생성하는 branch
- Naming : master, develop, release-*, hotfix-* 을 제외한 어떠한 이름도 허용가능
- 운용 기준

- develop 에서 branching 하며 완성되고 나면 다시 develop branch로 merging 한다.
- 새로 추가한 기능이 이점을 줄 수 있을때에만 develop branch로 merging한다.
- merging을 **완료**하고 나서 **생성된 feature branch를 삭제**한다.
- merging 시 "--no-ff" 옵션을 사용한다. 이 옵션은 merging할때 fast-forward와 함께진행될 때에도 항상 새로운 commit을 생성한다. 이로 인해 feature branch에서 저장했던 예전 작업들에 대한 정보들에 대한 손실을 막을 수 있다. 아래의 그림을 보면 그 차이가 드러난다. 오른쪽의 일반적인 merging은 feature에서 merging된 commit들이 기존에 develop에 있던 commit들과 구분이 안된다.  
      
    
    ![](https://t1.daumcdn.net/cfile/tistory/162CF72F4CC6259C64)
    
      
      
    

- **release**

- 새로운 release를 내기위해 준비하는 branch
- Naming : release-* (*는 니 맘대로 문자열을 의미한다.)
- 운용 방안

- develop branch로 부터 가져오고 develop와 master로 merging을 실시한다.
- **release branch 생성후 먼저 버전 올려주는 것**을 잊지 말자.
- minor bugs나 meta-data(버전정보, 빌드날짜 등등) 추가는 허용된다.
- 해당 번호 release시에 목표했던 feature들이 추가되어 만족할만한 기능이 나올때(develop branch가 다음release를 준비할 만한 상태일 때에...)에 release branch를 생성한다. 다음 릴리즈에서 포함되어야 되는 기능들은 절대로 포함시켜서는 안된다. 네이밍을 할때는 next-release같은 것은 피해야 한다. 그 대신 0.5, 1.2.3 같은 구체적인 수치와 그에 해당하는 기준들을 마련한다.
- 작업이 완료되면 master로 merging한다.merging 후에는 release정보로 바로 tagging한다. master로의 작업이 완료된 후에는 **반드시 develop에도 merging을 실시** 한다. merging시에 발생하는 conflict는 해결후 commit 한다.
- **merging이 완료되면 해당 release branch를 삭제**한다.  
      
    

- **hotfix**

- 출시된 제품에서 오류가 발견되어 즉시 해결해야 하는경우 이용하는 branch
- Naming : hotfix-*
- 운용 방안

- master의 해당 태그로부터 가져오고 develop과 master로 merging을 실시한다.
- **hotfix branch생성후 먼저 버전 올려주는 것**을 잊지 말자.
- 완료된 후에는 master 적용후 develop에도 적용해야 한다. 이때, release branch가 있는 경우 develop에 merging 하지 말고 release에 한다. 왜냐하면 release시에 테스트가 수반되고, release작업이 완료된 경우 release branch가 다시 develop에 적용되기 때문이다.
- **merging이 완료되면 해당 hotfix branch를 삭제**한다.