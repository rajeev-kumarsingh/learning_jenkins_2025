# Day-04: Tasks

1. Overview of Jenkins Architecture(done but need to review again)
2. Difference between freestyle jon and pipeline job in jenkins(done)
3. What is pipeline?
4. Which all phases are there in build.(compile,code-review, unit-testing, Integration Testing, Packaging/Artifact)(done)
5. Jenkins Installation Guide Review(Done)
6. Why Jenkins is popular amoung other methodology?(free, open-source, rich-of-plugins, community-support)(done)
7.

---

3. What is pipeline?

- Allow me to make an analogy to an assembly line used to manufacture a physical product.
  Any product goes through a series of steps before it is released to the customers.

  - Let's take a laptop, for example.

  - To oversimplify, the assembly line could have the following steps.

  - Take a laptop body case.

  - Add the mainboard.

  - Add the keyboard.

  - Do some quality assurance to ensure it turns on and works properly.

  - Put it in a box.

  - And then finally ship it to customers.

- Now we are not using Jenkins to produce physical product.We want to build software. However, producing software has many things in common to what I've just described.
- Let's try to build the laptop assembly line in Jenkins using a pipeline. Well, okay.
  Kind of. Instead of using real components, we're going to use a file folder and some text. One of the reasons we want to use Jenkins is to avoid doing manual work. So let's begin with the first task using a new laptop case. We're going to put this in a stage.

  - But first let's go ahead and create a completely new job. I'm going to create this job and call it `laptop assembly`.

  - And select pipeline as a style and click on okay. And want to jump directly here to the pipeline.

  - And we're going to start with the `Hello World` because this already gives us the structure. We're going to put everything that we need to do in a stage because we kind of like considering this, like building part.

  - We're putting all the components together.

  - You want to replace hear the word hello with build so that we know that this is the build stage.

  - Now, inside the steps there are a series of commands we need to run. So for example, we can still use the `echo` command. And we can have here a message like building a new laptop so that we know at this point we are starting the build process.Okay. So the first part is done.

- Now let's say that when we're building this laptop we want to store everything in a directory.
  So in order to store everything in a directory we actually need to create a directory.
  So we're going to use a shell command which is called `mkdir`. So this will create a new directory, Of course, to be able to use this command we need to use here `SSH`. And to run this as a shell command. Now make directory also takes an argument and the name of the argument is build.
  All right. So the first step is already done.

- Now let's say that we need to create a new file.
  So we want to create a file which is called `computer.txt`. And this file needs to be inside the build directory. For that we can use another shell command which is called `touch`.
  I'm going to use here ssh. What touch does `touch` is another Linux command which has a double function. It changes the date if the file exists.
  So you can see at the file when it has been lastly modified. Or if the file doesn't exist, it creates that file. And this is exactly what we want to do with this `touch` command. We want to create a new file. So we're going to put this file inside the build directory. And we're going to call it `computer.txt`. So it's build `/computer.txt`.
  This is where we're going to store all the components that we want to add to the laptop.
  All right. Now let's say this first part is done.
  And now we want to for example add the main board.
  So what we can do here is we can use the `echo` command to print the text, and then we can use an `operator`(>>) to append that text to a specific file.
