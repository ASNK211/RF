<template>
  <div>
    <div>
      <div class="shadow border-0">
        <button
          size="sm"
          @click.prevent="copyThreadInfoToClipboard('thread-id')"
          >Copy to clipboard</button
        >
        <div
          id="thread-id"
          class="text-monospace"
          v-for="thread in allThreads"
          :key="thread.threadName"
        >
          "{{ thread.threadName }}" #{{ thread.id }} state:{{
            thread.threadState
          }}
          cpu-time:{{ thread.cpuTime }} user-time:{{ thread.userTime }}
          <span v-if="thread.lockName != null"
            >Lock-name: {{ thread.lockName }} </span
          ><span v-if="thread.getLockOwnerName != null"
            >Lock-owner-name: {{ thread.getLockOwnerName }}</span
          >
          <br />
          <code id="line-break"> {{ thread.stacktrace }}</code>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      allThreads:[{
            "isThreadCpuTimeSupported": "true",
            "getLockOwnerName": null,
            "isSuspended": "false",
            "stacktrace": "java.base@11.0.5/java.net.PlainSocketImpl.accept0(Native Method)\njava.base@11.0.5/java.net.PlainSocketImpl.socketAccept(PlainSocketImpl.java:159)\njava.base@11.0.5/java.net.AbstractPlainSocketImpl.accept(AbstractPlainSocketImpl.java:458)\njava.base@11.0.5/java.net.ServerSocket.implAccept(ServerSocket.java:551)\njava.base@11.0.5/java.net.ServerSocket.accept(ServerSocket.java:519)\norg.apache.catalina.core.StandardServer.await(StandardServer.java:609)\norg.apache.catalina.startup.Catalina.await(Catalina.java:721)\norg.apache.catalina.startup.Catalina.start(Catalina.java:667)\njava.base@11.0.5/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)\njava.base@11.0.5/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)\njava.base@11.0.5/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)\njava.base@11.0.5/java.lang.reflect.Method.invoke(Method.java:566)\napp//org.apache.catalina.startup.Bootstrap.start(Bootstrap.java:343)\napp//org.apache.catalina.startup.Bootstrap.main(Bootstrap.java:474)\n",
            "cpuTime": "16312.5",
            "userTime": "11515.625",
            "threadState": "RUNNABLE",
            "id": "1",
            "lockName": null,
            "threadName": "main",
            "isNative": "true"
        },
        {
            "isThreadCpuTimeSupported": "true",
            "getLockOwnerName": null,
            "isSuspended": "false",
            "stacktrace": "java.base@11.0.5/java.lang.ref.Reference.waitForReferencePendingList(Native Method)\njava.base@11.0.5/java.lang.ref.Reference.processPendingReferences(Reference.java:241)\njava.base@11.0.5/java.lang.ref.Reference$ReferenceHandler.run(Reference.java:213)\n",
            "cpuTime": "0.0",
            "userTime": "0.0",
            "threadState": "RUNNABLE",
            "id": "2",
            "lockName": null,
            "threadName": "Reference Handler",
            "isNative": "false"
        },
        {
            "isThreadCpuTimeSupported": "true",
            "getLockOwnerName": null,
            "isSuspended": "false",
            "stacktrace": "java.base@11.0.5/java.lang.Object.wait(Native Method)\njava.base@11.0.5/java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:155)\njava.base@11.0.5/java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:176)\njava.base@11.0.5/java.lang.ref.Finalizer$FinalizerThread.run(Finalizer.java:170)\n",
            "cpuTime": "0.0",
            "userTime": "0.0",
            "threadState": "WAITING",
            "id": "3",
            "lockName": "java.lang.ref.ReferenceQueue$Lock@4f01e5fa",
            "threadName": "Finalizer",
            "isNative": "false"
        }]
    }
  }
  ,
  methods: {
    copyThreadInfoToClipboard(id) {
      var copyText = document.getElementById(id).innerHTML;
      var input_temp = document.createElement('textarea');
      input_temp.innerHTML = copyText;
      document.body.appendChild(input_temp);
      input_temp.select();
      input_temp.setSelectionRange(0, 99999); /*For mobile devices*/
      document.execCommand('copy');
      alert(input_temp.value);
    },
  },
};
</script>