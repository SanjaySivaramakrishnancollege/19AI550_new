# Ex.No: 10 – Implementation of Coin Collector 2D Game

### DATE: 24.05.2026  
### REGISTER NUMBER: 212223240151

---

# AIM

To develop a Coin Collector 2D Game using Unity Engine and implement player movement, coin collection, enemy interaction, score tracking, and winning conditions.

---

# Algorithm

```text
1. Install Unity Hub and create a new 2D Unity project.
2. Download the necessary game assets and sprites from online resources.
3. Import the assets into the Unity project.
4. Design the game environment using platforms, coins, enemies, and flag objects.
5. Create the player object and add Rigidbody2D and Collider2D components.
6. Develop the PlayerMovement script for player movement and jumping.
7. Add collectible coins and create a score management system.
8. Create enemy movement using SnailEnemy script.
9. Add invisible wall colliders for enemy patrol movement.
10. Create a DeathZone object to detect player falling.
11. Create a FinishFlag object to display winning message.
12. Design the UI using TextMeshPro for score and game messages.
13. Implement GameManager script to control score and game states.
14. Test the game and fix collisions, movements, and gameplay issues.
15. Run the game successfully.
```

---

# Program

## PlayerMovement.cs

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float speed = 5f;
    public float jumpForce = 14f;

    private Rigidbody2D rb;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();

        // Better gravity
        rb.gravityScale = 4f;
    }

    void Update()
    {
        // Move left/right
        float move = Input.GetAxis("Horizontal");

        rb.linearVelocity = new Vector2(
            move * speed,
            rb.linearVelocity.y
        );

        // Jump
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.linearVelocity = new Vector2(
                rb.linearVelocity.x,
                jumpForce
            );
        }

        // Small jump if key released early
        if (Input.GetKeyUp(KeyCode.Space))
        {
            if (rb.linearVelocity.y > 0)
            {
                rb.linearVelocity = new Vector2(
                    rb.linearVelocity.x,
                    rb.linearVelocity.y * 0.4f
                );
            }
        }
    }

    private void OnCollisionStay2D(Collision2D collision)
    {
        isGrounded = true;
    }

    private void OnCollisionExit2D(Collision2D collision)
    {
        isGrounded = false;
    }
}
```

---

## SnailEnemy.cs

```csharp
using UnityEngine;

public class SnailEnemy : MonoBehaviour
{
    public float speed = 2f;

    private bool movingRight = true;

    void Update()
    {
        // Move snail
        if (movingRight)
        {
            transform.Translate(Vector2.right * speed * Time.deltaTime);
        }
        else
        {
            transform.Translate(Vector2.left * speed * Time.deltaTime);
        }
    }

    // Turn around at invisible walls
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Wall"))
        {
            movingRight = !movingRight;

            Vector3 scale = transform.localScale;
            scale.x *= -1;

            transform.localScale = scale;
        }
    }

    // Player touches snail = GAME OVER
    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            GameManager.instance.ShowMessage("GAME OVER!");
        }
    }
}
```

---

## Coin.cs

```csharp
using UnityEngine;

public class Coin : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Player"))
        {
            GameManager.instance.AddScore(1);

            Destroy(gameObject);
        }
    }
}
```

---

## GameManager.cs

```csharp
using TMPro;
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;

    public TextMeshProUGUI scoreText;
    public TextMeshProUGUI messageText;

    void Awake()
    {
        instance = this;
    }

    void Start()
    {
        UpdateScore();

        messageText.text = "";
    }

    public void AddScore(int amount)
    {
        score += amount;

        UpdateScore();
    }

    void UpdateScore()
    {
        scoreText.text = "Score: " + score;
    }

    public void ShowMessage(string message)
    {
        messageText.text = message;

        // Stop game
        Time.timeScale = 0f;
    }
}
```

---

## FinishFlag.cs

```csharp
using UnityEngine;

public class FinishFlag : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Player"))
        {
            GameManager.instance.ShowMessage("YOU WIN!");
        }
    }
}
```

---

## DeathZone.cs

```csharp
using UnityEngine;

public class DeathZone : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Player"))
        {
            GameManager.instance.ShowMessage("YOU FELL!");
        }
    }
}
```

# Output
<img width="1520" height="1025" alt="image" src="https://github.com/user-attachments/assets/da142f0e-63e6-4281-b863-7a867883cbd4" />
<img width="1486" height="997" alt="image" src="https://github.com/user-attachments/assets/e228eecf-d03a-4ff6-8fd8-510b8b1c4b75" />
<img width="1486" height="1027" alt="image" src="https://github.com/user-attachments/assets/43355b3e-6dbf-4fad-8ee4-f39100fa15a7" />


# Result

Thus the Coin Collector 2D Game was successfully developed using Unity Engine and basic Artificial Intelligence techniques for enemy movement and gameplay interaction.
