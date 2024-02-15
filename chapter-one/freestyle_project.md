# Freestyle Projects

Freestyle ("chained") projects (also called **jobs**) have been used to define the build flow almost from the day Jenkins was born.

> [!WARNING]
> Freestyle jobs are still supported and are useful in specific situations but are **not recommended** for most new developments.

Freestyle jobs only provide sequential steps, are not defined in code, and do **not provide centralized configuration**.

Many continuous objectives cannot be solved or, at best, are very difficult to implement with Freestyle due to:

- Requires (complex) conditional logic
    - Often, we do not want to simply say run job A, then run job B after Job A is finished, and follow it with job C. In real-world situations, things are more complicated than that.
- Requires resource allocation and cleanup
- Involves human interaction for manual approval
- Should be resumable at some point on failure
    - Some deployment flows run for a couple of hours or even days. If the hardware fails along the way, we need a mechanism to restart the deployment flow from a defined place rather than having to rerun it from the beginning.