# Gamer F

This challenge (along with Gamer R) requires a bit of research into the Unity Hacking community. Not a lot of stuff you can do in the game.
The first applciation to download is dnSpy. This allows you to look into the dll files and edit code. Load up `Assembly-CSharp.dll`.
After looking through the classes you can get 2 parts of the flag.

**Part 1**
![](https://i.gyazo.com/837493d153dc130e48106d9f45b4c63b.png)

```
In the UIManager class, we can check the ChangeOpacity method and we see there is a cover covering up the flag.
My solution was to just add an extra 0f argument, making it new Color(v,v,v,0f) which changes opacity to 0.
```

![](https://i.gyazo.com/8d46d6db8fafe5a0896406d718934fe4.png)