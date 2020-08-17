# Sculpture
A virtual sculpture program based on minecraft
I am french and I am not at ease with english language, but I hope this text will remain  understandable.

My motivation

I tried to learn Three.js for many months thanks to the wonderful tutorials of Three.js 	Fundamentals, and I am particularly 	interested in the Making Voxel Geometry demo.
I've tried to  modify it toward a program that allows virtual sculpture. I still don't know if this 	purpose  make sense but I would like to improve the program as far as possible, and I am 	now confronted with two issues that exceed my knwoledge : I don't know if my work is 	worth of  interest, but if so I would be grateful for any help.

How to use the program

Some explanations on how the program works may be useful before expressing these issues.

The basic idea is to take photos of an object from front, back, etc. , and put them together to build 	an image I can project as a texture on a block of voxels : it's not ever possible, and when it is 	not easy to take photos that fit in a suitable way.
There are four images available at each corner of the sculpture.html displayed page, and you may 	click on the one you want.

At first there are two ways to display the object :
click on the « new » button to display the initial rough block.
click on the « old » button to display the most refined sculpture, which is stored in the program body.

There are five radio buttons « h1 » ... « h5 » which allow you to choose the number of voxels on 	each side of the block : by default h1 value is 1, and the following are increased by a factor 8 	at each step. 
In some cases you choose the desired level (« new » button for instance), in others it is 	automatically updated (« old » button for instance).

When starting with any level you may :
delete one voxels : by clicking on the voxel just as you did in your tutorial;
delete many voxels : by clicking on the voxel and holding the « ctrl » key the deletion is iterated in the direction of the face's normal;
add one voxels :  by clicking on the voxel and holding the « shift » key;
add many voxels: by clicking on the voxel and holding the «alt» key the addition is iterated in the direction of the face's normal;
The iteration process is sensitive: you must shoot fine.
The addition action is intended only to cancel the previous deletions : I have disabled the 	opportunity of adding extra voxels since it doesn't make sense.

The main tools are the « up » and « down » buttons which allow you to store the previous session of 	del / add and rises or decreases automatically the level « h » to the nearest level : 
using the « up » button you can progressively polish the initial block;
using the « down » button you may return to the previous level if you've forgotten to delete big voxels. This last possibility because it becomes rather tedious to delete voxels at the 4th or 5th levels.

Each h-level owns its session in the indexedDB storage : the « set » and « get » buttons allow to 	store or load these sessions independently of the « up » and « down » buttons.

Finally the « save » and « load » buttons allow you to store or load the entire voxel world in the 	locastorage, as a string : this because it was the only way I've found to copy the result and 	paste it in the program body.

My issues

Now my two issues :
first the 3D effect I hoped from my sculpted block is not so convincing when looking at 	front : not bad but the difference between its aspect and the initial block could have 	been more spectacular. May be this because of a bad use of lights or materials : I 	don't know how to improve that.
second when rotating the sculpted block the edges are not so nice, and I would like to smooth these edges : I've seen that webGL may allow this trick, but webGL  is over my comprehension scope and I wondered if that was possible with Three.js only And anyway how to project the image since there would be no more front/left/ etc. faces ?
I would also be grateful for all advices to improve the program, especially how to decrease the 	execution time when searching voxels.

Some technical tricks

One word about the structure of the block : its proportions are setted from the image (in another 	program) as an array R = [rx,ry,rz], which is stored in the SCULPTURE object; then R is 	multiplied by the h-level factor to obtain the right number S = [sx,sy,sz] of voxels.
I've preserved the fundamental structure of Making Voxel Geometry but have changed many names and added 	many procedures. 
I tried to add comments: I suppose you will quickly understand by your own what I hardly try to 	explain.
Global variables or constants outside the main procedure are uppercased ; they are underscored 	inside this procedure. 
The 'main' parameters are 'R_' , which is equal to the current proportion array, and 'name_', which is 	equal to the current name of the image, as stored in the SCULPTURE or RECORDS objects.
Another useful variable is 'h_', which is equal to the current h-level.
You must remove the slashes before the handleIDB() assertion to create the indexedDB base at first 	execution.

Bugs

Of course there may be some/many/a lot of/ bugs in this program.
One I identified and did not succeed to repair : when changing the image by clicking on thumbnails 	it seems that the previous image name is memorized in the 'handleIDB' function; 	consequently the 'newWorld' function erases two IDB files instead of the only one that 	should be, in the 'name_' variable. Similar bugs with the 'oldWorld' and 'loadWorld' 	functions. 
	Since these bugs don't appear when refreshing the page it's probably because these functions 	callback the 'main' function from inside : I've tried to use event.stopPropagation() and 	db.close() orders without success.
