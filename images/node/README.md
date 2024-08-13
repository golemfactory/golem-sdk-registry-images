# Golem Node.js VM Images

## Supported versions

* [latest](Dockerfile.latest)
* [20](Dockerfile.20), [20-alpine](Dockerfile.20-alpine)
* [18](Dockerfile.18), [18-alpine](Dockerfile.18-alpine)

## Usage

Minimal `golem-js` based example:

```ts
import { GolemNetwork } from "@golem-sdk/golem-js";

const glm = new GolemNetwork();

await glm.connect();

try {
  const rental = await glm.oneOf({
    order: {
      demand: {
        workload: {
          imageTag: "golem/node:latest",
        },
      },
      market: {
        rentHours: 1,
        pricing: {
          model: "linear",
          maxStartPrice: 0,
          maxEnvPerHourPrice: 0.25,
          maxCpuPerHourPrice: 0.25,
        },
      },
    },
  });

  const exe = await rental.getExeUnit();

  const result = await exe
    .run("node --version")
    .then((res) => res.stdout?.toString().trim());

  console.log("Result", result);
} catch (err) {
  console.error("Failed to run work on Golem", err);
} finally {
  await glm.disconnect();
}
```

## Added volumes

The following volumes are added to the base image from DockerHub, and allow you to upload files into them:

* `/golem/input`
* `/golem/output`
* `/golem/work`