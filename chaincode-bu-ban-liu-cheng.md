# Chaincode 部版流程

以下將說明如何將我們開發完的chaincode部屬至測試環境進行測試

> * Step 1 : 將chaincode人工搬檔至10.95.42.63:22\(Jenkins所在的位置\)
>
> * Step 2 : 從瀏覽器進入10.95.42.63:8080\(Jenkins console頁面\)
>
> * Step 3 : 跑測試的Install script，此動作將進行搬檔，就我們目前測試機的節點來說，即是將step 1我們放置在Jenkins server的chaincode搬到10.95.42.64這個測試環境的節點
>
> * Step 4 :
>
>   * Scenario 1 \(全新的chaincode，第一次install\)
>     * 使用Swagger或是putty連到10.95.42.64的其中一個volume跑instantiate的腳本
>   * Scenario 2 \(非全新的chaincode，只需進行upgrade\)
>     * 可以直接在Jenkins console裡面跑upgrade的腳本\(但instantiate和upgrade的腳本其實是做一樣的事情\)
>
> * Step 5 : 到Jenkins console，跑測試環境的Stop old version of chaincode
>
> * Step 6 : Done! Go to Swagger and try it out!



