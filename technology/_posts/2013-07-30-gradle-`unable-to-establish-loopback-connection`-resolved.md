---
layout: techpost
title: Gradle `Unable to establish loopback connection` resolved
---

So all of a sudden I began having issues with Gradle 1.6 builds failing, and this time not because of my code. I was getting errors like this:

    org.gradle.process.internal.ExecException: Timeout after waiting 120.0 seconds for Gradle Worker 6 (STARTED, running: true) to connect.
            at org.gradle.process.internal.DefaultWorkerProcess.doStart(DefaultWorkerProcess.java:137)
            at org.gradle.process.internal.DefaultWorkerProcess.start(DefaultWorkerProcess.java:114)
            at org.gradle.api.internal.tasks.testing.worker.ForkingTestClassProcessor.processTestClass(ForkingTestClassProcessor.java:63)
            at org.gradle.api.internal.tasks.testing.processors.RestartEveryNTestClassProcessor.processTestClass(RestartEveryNTestClassProcessor.java:45)
            at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
            at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
            at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
            at java.lang.reflect.Method.invoke(Method.java:601)
            at org.gradle.messaging.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:35)
            at org.gradle.messaging.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:24)
            at org.gradle.messaging.dispatch.FailureHandlingDispatch.dispatch(FailureHandlingDispatch.java:29)
            at org.gradle.messaging.dispatch.AsyncDispatch.dispatchMessages(AsyncDispatch.java:132)
            at org.gradle.messaging.dispatch.AsyncDispatch.access$000(AsyncDispatch.java:33)
            at org.gradle.messaging.dispatch.AsyncDispatch$1.run(AsyncDispatch.java:72)
            at org.gradle.internal.concurrent.DefaultExecutorFactory$StoppableExecutorImpl$1.run(DefaultExecutorFactory.java:66)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:722)
    Could not accept remote connection.
    org.gradle.internal.UncheckedException: java.io.IOException: Unable to establish loopback connection
            at org.gradle.internal.UncheckedException.throwAsUncheckedException(UncheckedException.java:39)
            at org.gradle.messaging.remote.internal.inet.SocketConnection.<init>(SocketConnection.java:58)
            at org.gradle.messaging.remote.internal.inet.TcpIncomingConnector$Receiver.run(TcpIncomingConnector.java:119)
            at org.gradle.internal.concurrent.DefaultExecutorFactory$StoppableExecutorImpl$1.run(DefaultExecutorFactory.java:66)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:722)
    Caused by: java.io.IOException: Unable to establish loopback connection
            at sun.nio.ch.PipeImpl$Initializer.run(PipeImpl.java:125)
            at sun.nio.ch.PipeImpl$Initializer.run(PipeImpl.java:69)
            at java.security.AccessController.doPrivileged(Native Method)
            at sun.nio.ch.PipeImpl.<init>(PipeImpl.java:141)
            at sun.nio.ch.SelectorProviderImpl.openPipe(SelectorProviderImpl.java:50)
            at java.nio.channels.Pipe.open(Pipe.java:150)
            at sun.nio.ch.WindowsSelectorImpl.<init>(WindowsSelectorImpl.java:126)
            at sun.nio.ch.WindowsSelectorProvider.openSelector(WindowsSelectorProvider.java:44)
            at java.nio.channels.Selector.open(Selector.java:227)
            at org.gradle.messaging.remote.internal.inet.SocketConnection$SocketInputStream.<init>(SocketConnection.java:135)
            at org.gradle.messaging.remote.internal.inet.SocketConnection.<init>(SocketConnection.java:56)
            ... 5 more
    Caused by: java.io.IOException: An existing connection was forcibly closed by the remote host
            at sun.nio.ch.SocketDispatcher.read0(Native Method)
            at sun.nio.ch.SocketDispatcher.read(SocketDispatcher.java:43)
            at sun.nio.ch.IOUtil.readIntoNativeBuffer(IOUtil.java:225)
            at sun.nio.ch.IOUtil.read(IOUtil.java:198)
            at sun.nio.ch.SocketChannelImpl.read(SocketChannelImpl.java:359)
            at sun.nio.ch.PipeImpl$Initializer.run(PipeImpl.java:108)
            ... 15 more


Turns out that Windows Anti-Virus was preventing `Java 1.7.0_21` from doing any networking, presumably due to some security problem. Changing `JAVA_HOME` to `1.7.0_25` did the trick.
