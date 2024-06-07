# Nether portals

Nether portals are used in Minecraft to travel between the nether and the overworld. In the nether every block traveled is 8 blocks horizontally, so you can use the nether to travel faster in the overworld.

## 2-in-1 portal

Besides traveling fast, you can also do something funky with a nether portal: You can create a single portal that teleports you to two locations in the overworld. I've written this out in case it's ever helpful.

So let's start with 2 portals at random locations in the overworld. We have a portal A at (ax, ay, az). We have a portal B at (bx, by, bz). We'd want to connect these with another portal in the nether.

You also need the blocks on which you stand in the portal in the nether to access the portals in the overworld, so we have the following:

- Portal A \\((ax, ay, az)\\)
- Portal B \\((bx, by, bz)\\)
- Block access A (block N) \\((nx, ny, nz)\\)
- Block access B (block M) (\\(mx, my, mz)\\)

Your nether portal will link with the center portal in the nether if the following statements are true:

\\[ (8nx-ax)^2 + (ny-ay)^2 + (8nz-az)^2 < (8nx-bx)^2 + (ny-by)^2 + (8nz-bz)^2 \\]

\\[ (8mx-bx)^2 + (my-by)^2 + (8mz-bz)^2 < (8mx-ax)^2 + (my-ay)^2 + (8mz-az)^2 \\]

In these equations it distills to N is closer to A than to B and M is closer to B than A. If you'd want to make the calculations simpler, you can try to have one coordinate to be the same, this way you can remove any statement with that coordinate in it.