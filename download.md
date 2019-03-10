# 下载

## 原因

1. 因为js常规的异步加载过程中，数据的传输方式往往是ajax的异步加载，但是因为ajax不支持数据流，所以无法通过它实现下载功能。
2. 一般情况下，同问window.open()或者location.open()来打开一个全新的页面直接跳转下载。但是这种做法的最大问题在于，如果下载的文件需要发送请求头来做一个权限验证，那么直接通过打开新页面的方式是无法实现的。
3. 所以通过BLOB对象是一个非常有效的处理方式。

## BLOB

1. Blob 对象表示一个不可变、原始数据的类文件对象。
2. File 接口基于Blob，继承了 blob 的功能并将其扩展使其支持用户系统上的文件。
3. FileReader 对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 File 或 Blob 对象指定要读取的文件或数据。

## demo片段

```js
      async downloadAll (num) {
                    //   开始下载

                    //   后端提供的下载地址
                    let url = 'location/get-location?race_id=' + localStorage.getItem('raceId') + '&export=' + num;

                    //  异步函数，必须要等待ajax请求完成以后，在进行后续操作。同时将在发送请求前，将返回数据的数据类型，设置为blob
                    let res = await this.$ajax({
                        url,
                        responseType: 'blob'
                    });

                    let resBlob = res.data;
                    let resData = null;
                    try {
                        let resText = await new Promise((resolve, reject) => {
                            // 通过 FileReader 接受并解析
                            let reader = new FileReader();
                            //  abort 读取操作被中断时触发
                            reader.addEventListener('abort', reject);
                            // error 读取操作出现错误时触发
                            reader.addEventListener('error', reject);
                            // loaded 读取操作结束(无论成功还是失败)时触发
                            reader.addEventListener('loadend', () => {
                                resolve(reader.result);
                            });
                            // 文件
                            reader.readAsText(resBlob);
                        });
                        // JSON
                        resData = JSON.parse(resText);
                    } catch (err) {
                        console.log(err);
                    }
                    let download = window.URL.createObjectURL(resBlob);
                    let link = document.createElement('a');
                    link.href = download;
                    let date = new Date();
                    let year = date.getFullYear();
                    let month = date.getMonth() + 1;
                    let day = date.getDate();
                    link.setAttribute('download', 'title' + year + '-' + month + '-' + day + '.csv');
                    // link.setAttribute('download', title);
                    document.body.appendChild(link);
                    link.click();
            }
```