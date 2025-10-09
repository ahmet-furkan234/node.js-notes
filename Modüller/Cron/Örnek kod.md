
```ts
import { TkMessage } from "../utils/tkMessage.js";

import cron from "node-cron";

export class CronService {
  public async startCronJobs(): Promise<void> {
    cron.schedule("*/10 * * * * *", () => {
      TkMessage.info("10 saniyelik cron çalıştı");
    });

    cron.schedule("*/30 * * * * *", () => {
      TkMessage.success("30 saniyelik cron çalıştı");
    });

    cron.schedule("*/1 * * * *", () => {
      TkMessage.warning("60 saniyelik cron çalıştı");
    });
    TkMessage.success("Cron servisi başlatıldı");
  }
}
```