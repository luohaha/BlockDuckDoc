---
icon: sliders-simple
---

# Configs setting

### How to use

You can use pragma which like:

```sql
pragma blockduck_set_configs('MAX_BLOCK_CNT_PER_FETCH', 100)
```

to update the configs of BlockDuck.

#### **inputs**

| Args         | Types   |
| ------------ | ------- |
| config name  | VARCHAR |
| config value | BIGINT  |

Configs available for modification:

| Config Name                 | Info                                                                                            |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| MAX\_BLOCK\_CNT\_PER\_FETCH | Define the maximum number of blocks that can be processed per scan in a table function.         |
| MAX\_HTTP\_BATCH\_CNT       | Define the maximum number of HTTP requests that can be batch sent within a single HTTP request. |

