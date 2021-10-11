## JPA and Hibernate Cascade Types

One To One

```java
@Entity
@Table(name="posts")
public class Post {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;

    @OneToOne(mappedBy = "post", cascade = CascadeType.ALL, orphanRemoval = true)
    private PostDetails details;
	
    public void addDetails(PostDetails details) {
        this.details = details;
        details.setPost(this);
    }

    public void removeDetails() {
        if (details != null) {
            details.setPost(null);
        }
        this.details = null;
    }
}

@Entity
@Table(name="post_details")
public class PostDetails {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;

    @OneToOne
    @PrimaryKeyJoinColumn
    private Post post;
}
```
Many To One 

```java
@Entity
@Table(name="items")
public class Items {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;

    @ManyToOne
    @JoinColumn(name="cart_id", nullable=false)
    private Cart cart;

    public Items() {}
}
```

One To Many

```java
@Entity
@Table(name="cart")
public class Cart {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;

    @OneToMany(mappedBy = "cart", cascade = CascadeType.ALL, orphanRemoval = true)
    private Set<Items> items;
}
```

Many To Many

```java
@Entity
@Table(name="students")
class Student {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;
    
    @ManyToMany(fetch = FetchType.EAGER, cascade = {CascadeType.PERSIST, CascadeType.MERGE})
    @JoinTable(name = "course_like", joinColumns = @JoinColumn(name = "student_id"), inverseJoinColumns = @JoinColumn(name = "course_id"))
    Set<Course> likedCourses;
}

@Entity
@Table(name="courses")
class Course {
    @Id @GeneratedValue(strategy = GenerationType.AUTO) private Long id;
	
    @ManyToMany(mappedBy = "likedCourses", cascade = {CascadeType.PERSIST, CascadeType.MERGE})
    Set<Student> likes;
}
```
