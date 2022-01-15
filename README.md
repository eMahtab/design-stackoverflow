# Design Stackoverflow

## System requirements :

We will be designing a system with the following requirements:

1. Any non-member (guest) can search and view questions. However, to add or upvote a question, they have to become a member.
2. Members should be able to post new questions.
3. Members should be able to add an answer to an open question.
4. Members can add comments to any question or answer.
5. A member can upvote a question, answer or comment.
6. Members can flag a question, answer or comment, for serious problems or moderator attention.
7. Any member can add a bounty to their question to draw attention.
8. Members will earn badges for being helpful.
9. Members can vote to close a question; Moderators can close or reopen any question.
10. Members can add tags to their questions. A tag is a word or phrase that describes the topic of the question.
11. Members can vote to delete extremely off-topic or very low-quality questions.
12. Moderators can close a question or undelete an already deleted question.
13. The system should also be able to identify most frequently used tags in the questions.


## Account, AccountStatus, Member, Admin, Moderator
```java
// For simplicity, we are not defining getter and setter functions. The reader can
// assume that all class attributes are private and accessed through their respective
// public getter methods and modified only through their public methods function.

public class Account {
  private String id;
  private String password;
  private AccountStatus status;
  private String name;
  private Address address;
  private String email;
  private String phone;
  private int reputation;

  public boolean resetPassword();
}

public enum AccountStatus{
  ACTIVE,
  CLOSED,
  CANCELED,
  BLACKLISTED,
  BLOCKED
}

public class Member {
  private Account account;
  private List<Badge> badges;

  public int getReputation();
  public String getEmail();
  public boolean createQuestion(Question question);
  public boolean createTag(Tag tag);
}

public class Admin extends Member {
  public boolean blockMember(Member member);
  public boolean unblockMember(Member member);
}

public class Moderator extends Member {
  public boolean closeQuestion(Question question);
  public boolean undeleteQuestion(Question question);
}
```

# Bounty
```java
public class Bounty {
  private int reputation;
  private Date expiry;

  public boolean modifyReputation(int reputation);
}
```

# Question and QuestionStatus
```java
public class Question{
  private String title;
  private String description;
  private int viewCount;
  private Date creationTime;
  private Date updateTime;
  
  private QuestionStatus status;
  private Member askingMember;
  private Bounty bounty;
  
  private List<Comment> comments;
  private List<Answer> answers;

  public boolean close();
  public boolean undelete();
  public boolean addComment(Comment comment);
  public boolean addBounty(Bounty bounty);

}

public enum QuestionStatus{
  OPEN,
  CLOSED,
  ON_HOLD,
  DELETED
}
```

# Badge, Tag, Notification
```java
public class Badge {
  private String name;
  private String description;
}

public class Tag {
  private String name;
  private String description;
}

public class Notification {
  private int notificationId;
  private Date createdOn;
  private String content;

  public boolean sendNotification();
}

```
# Comment, Answer
```java
public class Comment {
  private String text;
  private Date creationTime;
  private int flagCount;
  private int voteCount;

  private Member commentedBy;

  public boolean incrementVoteCount();
}

public class Answer {
  private String answerText;
  private Date creationTime;
  private boolean isAccepted;
  private int voteCount;
  private int flagCount;
  
  private Member answeredBy;
  
  public boolean incrementVoteCount();
}

```

# References :
https://www.educative.io/courses/grokking-the-object-oriented-design-interview/m2YWoEq06AR

https://www.youtube.com/watch?v=eTB0nxb-j-Q
