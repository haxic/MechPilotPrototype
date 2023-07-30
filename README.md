# MechPilotPrototype
A Unity prototype / sandbox project

The .zip file contains a built project that is ready to run.

Unpack and run the .exe file -> press Host/Server to start a client as host or dedicated server.

Can run the .exe file again to start another client that joins the first one.

This prototype is not here to show anything cool. It's just an old sandbox project used for learning Unity.


Some short design descriptions:

Multiplayer is achieved with Netcode for GameObjects. Player logic is client-authoritative. Movement/physics is synchronized through built-in snapshot interpolation. Actions like spawning vehicle and shooting is done through RPC calls. Projectiles are not continuously synchronized, they are only synchronized when spawned. Naturally, since it takes time for the projectile to be distributed to the server and other clients, the projectile would either be spawned in an unnatural position or would have a trajectory not aligned with the spawning client (depending on how the initial implementation would be). To fix this, the spawning client attach spawn data to the projectile, it's original location and trajectory, such that the server/other clients can spawn it the shooting vehicle's weapon and overtime adjust the trajectory so it matches the original spawn point and trajectory. The purpose of doing it like that is to minimize data transfers - to not continuously synchronize projectiles.

MeshBaker is used to bake buildings into one mesh in order to improve performance - a building contains a lot of meshes and would lag without the baking.

AI is implemented by having an "AI agent" separated from the vehicle/tank it controls. An agent move around on the map like an invisible mousepointer and commands the vehicle to move towards it (while keeping a very short leash in order not to make the vehicle get stuck in stuff).
