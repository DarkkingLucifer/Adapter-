# Adapter-通用模板

private XxAdapter adapter;

adapter = new XxAdapter(context, list);



 private void initView() {
        employeeService = new EmployeeService(this);
        itemList = new ArrayList<>();
        shopId = mApplication.getCurrShopId() + "";
        adapter = new SpecialTimeAdapter(mActivity, itemList);
        rvSpecialTime.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false));
        rvSpecialTime.setAdapter(adapter);
    }
    private void requestData() {
        addDisposableIoMain(employeeService.listWeekRebateRate(shopId), new DefaultConsumer<List<WeekRebateRateBean>>(mApplication) {
            @Override
            public void operateSuccess(BaseResult<List<WeekRebateRateBean>> data) {
                itemList.clear();
                itemList.addAll(data.getData());
                adapter.notifyDataSetChanged();
            }
        });
    }
