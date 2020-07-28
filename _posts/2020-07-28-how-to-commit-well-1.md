---
title: "Git 잘 쓰기 - Commit은 어떻게 해야할까"
date: 2020-07-28 11:50:00 -0400
categories: git
---

# 커밋은 어떻게 해야하지?

## (1) 어떤 단위로 Commit을 해야할까

+ Gerrit 같은 리뷰 시스템이 포함된 저장소를 사용하는 경우, 하나의 Commit은 하나의 Review 단위가 된다. 너무 방대한 양을 한꺼번에 Commit하는 것은 Reviewer에게 실례일 수 있다.
+ 커밋은 논리적으로 구분되며 일관성이 있어야 한다. 일반적으로 최소 단위별로 되어야 한다. (Atomic)


## (2) 어떤 것을 Commit해야 할까

+ 반드시 테스트를 통과한 후 커밋을 수행해야 한다. 즉, 테스트 중 발견된 문제가 다 수정된 다음에 커밋을 해야한다. 다시 말해, 커밋한 다음 "이전 커밋 후 테스트에서 발견된 문제 수정"이라는 별도의 커밋이 있으면 안된다.
+ 최소 단위로 해야한다. 규모가 큰 리팩토링은 기능 수정과는 별도로 해야한다. 기능 수정과 리팩토링을 동시에 하는 것은 지양한다.
+ 코드를 원래 있던 파일에서 다른 파일로 옮기는 것은 별도의 커밋으로 진행한다. 기능 수정과 동시에 하거나, 해당 파일의 리팩토링을 함께 하는 것도 지양한다.


## (3) 기타 고려 사항

+ 과도하게 세분화된 커밋은 Squash를 통해 합칠 수 있다. 하지만 덩어리로 커밋된 건 나중에 가서 나눌 수 없다. 차라리 가능하면 작은 단위로 커밋을 하고, 나중에 합치는 게 낫다고 판단될 때 합치는 게 낫다.  

  
  
# 커밋 메시지를 잘 쓰자

## (1) 커밋 메시지의 Subject는 명령문으로 시작하여 짧게 쓰기

+ 짧게 : 50자 내외
+ Subject의 첫 글자는 대문자로 한다
+ 명령문 : 현재 시제의 명령문으로 시작하여 단순하게 설명하기
+ 어떤 것을 커밋했는지 간단히 쓰기
    - (예) '서브시스템이름' : 커밋 제목 → 'submodule' : Update blah blah

| 좋은 예 | 나쁜 예 |
|:---:|:---:|
|<code>$ git log --oneline -5 --author pwebb --before "Sat Aug 30 2014"
  5ba3db6 Fix failing CompositePropertySourceTests
  
  84564a0 Rework @PropertySource early parsing logic
  e142fd1 Add tests for ImportSelector meta-data<br><br>887815f Update docbook dependency and generate epub
  ac8326d Polish mockito usage</code>|<code>$ git log --oneline -5 --author cbeams --before "Fri Mar 26 2009" 
  
  e5f4b49 Re-adding ConfigurationPostProcessorTests after its brief removal in r814. @Ignore-ing the testCglibClassesAreLoadedJustInTimeForEnhancement() method as it turns out this was one of the culprits in the recent build breakage. The classloader hacking causes subtle downstream effects, breaking unrelated tests. The test method is still useful, but should only be run on a manual basis to ensure CGLIB is not prematurely classloaded, and should not be run as part of the automated build.
  2db0f12 fixed two build-breaking issues: + reverted ClassMetadataReadingVisitor to revision 794 + eliminated ConfigurationPostProcessorTests until further investigation determines why it causes downstream tests to fail (such as the seemingly unrelated ClassPathXmlApplicationContextTests)
  147709f Tweaks to package-info.java files<br>22b25e0 Consolidated Util and MutableAnnotationUtils classes into existing AsmUtils
  7f96f57 polishing </code>|
    
## (2) Subject와 Content간의 blank line 두기

+ Blank line을 두게되면, --oneline 옵션으로 볼 때에 Subject만 출력된다.
+ Blank line이 없으면 메시지 전체가 출력되어 가독성이 떨어진다

## (3) 내용

+ 문장을 끝낼 때 마침표 찍지 않기
+ 한 줄에는 최대 72자 (또는 76자 내외로 하라는 가이드도 많다)
+ 내용에는 꼭 '무엇(what)', '왜(why)' 그리고 '어떻게(how)'를 설명하자.
    - 무엇(what)을 변경했는지
    - 왜(why) 변경했는지
    - 어떻게(how) 변경했는지
+ 자동화된 시험 외에 수행한 매뉴얼 테스트가 있다면 설명해주자
+ 성능 향상과 관련된 경우라면, 간략한 테스트 결과를 넣어주는 것도 좋다

  
  
## References
+ https://tech.10000lab.xyz/git/git-commit-discipline.html
+ https://chris.beams.io/posts/git-commit/
