# Nether portals

Nether portals are used in Minecraft to travel between the nether and the overworld. In the nether every block traveled is 8 blocks horizontally, so you can use the nether to travel faster in the overworld.

## 2-in-1 portal

Besides traveling fast, you can also do something funky with a nether portal: You can create a single portal that teleports you to two locations in the overworld. I've written this out in case it's ever helpful.

So let's start with 2 portals at random locations. We have a portal A at (ax, ay, az). We have a portal B at (bx, by, bz).

You also need the blocks on which you stand to access the portal, so we have the following:

- Portal A `(ax, ay, az)`
- Portal B `(bx, by, bz)`
- Block access A (block N) `(nx, ny, nz)`
- Block access B (block M) `(mx, my, mz)`

Your nether portal will link with the center portal in the nether if the following statements are true:

```
(8nx-ax)² + (ny-ay)² + (8nz-az)² < (8nx-bx)² + (ny-by)² + (8nz-bz)²

(8mx-bx)² + (my-by)² + (8mz-bz)² < (8mx-ax)² + (my-ay)² + (8mz-az)²
```

In these equations it distills to N is closer to A than to B and M is closer to B than A. If you'd want to make the calculations simpler, you can try to have one coordinate to be the same, this way you can remove any statement with that coordinate in it.