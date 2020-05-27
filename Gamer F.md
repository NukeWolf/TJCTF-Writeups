# Gamer F

Overall, not to hard when you have the tools but a bit tedious. This challenge (along with Gamer R) requires a bit of research into the Unity Hacking community. Not a lot of stuff you can do in the game.
The first applciation to download is dnSpy. This allows you to look into the dll files and edit code. Load up `Assembly-CSharp.dll`.
After looking through the classes you can get 2 parts of the flag.

**Part 1**

In the TetrisManager class, there is a method called CheckLineCompletion() which will print out the first part of the flag. 
We get this code:

```c#
if (this.score == 80)
	{
	string text = "506172742031206f6620666c61673a20746a6374667b77683372735f";
	string text2 = "";
	for (int l = 0; l < text.Length; l += 2)
		{
		text2 += ((char)byte.Parse(text.Substring(l, 2), NumberStyles.HexNumber)).ToString();
		}
	this.messageText.text = text2;
	this.soundManager.Play("Win Sound");
	}
```
Recompile and get the first part, **tjctf{wh3rs_**

**Part 3**

```
In the UIManager class, we can check the ChangeOpacity method and we see there is a cover covering up the flag.
My solution was to just add an extra 0f argument, making it new Color(v,v,v,0f) which changes opacity to 0.
```
![](https://i.gyazo.com/837493d153dc130e48106d9f45b4c63b.png)

![](https://i.gyazo.com/8d46d6db8fafe5a0896406d718934fe4.png)
Part 3 of flag : **_sn4ekk}**

**Part 2**

Part 2 wasn't as obvious. There was nothing in the code that referenced it.
I downloaded another application called Unity Assets Bundle Extractor which allowed me to view resources.

![](https://i.gyazo.com/7b1de77998bfaeab48d2eec938d7c4c0.png)

I noticed 4 sound files, which was weird because only 3 played in the game. 
Looking into the SoundManager class, we can see that sounds used are loaded into an array `sounds` and also the play method
which would play sounds based off a string name given. 

![](https://i.gyazo.com/d864344efcc8109e97d5fa8bdd156618.png)

To get the name of the sound I changed code in the TickUpdate Method in the SnakeMovement class to do things when I ran into fruit.
```c#
this.fruitColleced++;
this.fruitScoreText.text = string.Concat(this.fruitColleced);
```
to
```c#
this.fruitColleced++;
this.fruitScoreText.text = this.soundManager.sounds[3].name;
```
![](https://i.gyazo.com/701076daeeae8fa09ac6dfa958a39370.png)
We can then play the sound with
```c#
this.soundManager.Play("Less Cool Win Sound")
```
and get the middle part of flag.

**Flag:** `tjctf{wh3rs_the_T5sp1n_sn4ekk}`


