# JavaDeleteFile
这是Java做的一个小工具，但思想为删除一个文件或者文件夹而来，不局限语言。
# 使用方法及代码
 FileManage fileManage = new FileManager();
 FileManage.DelStatusListen delStatusListen = new FileManage.DelStatusListen() {

            long del = 0, found = 0;
            @Override
            public void foundCount(long count) {
                found = count;
                System.out.println("发现" + count + "个文件");
                lbFoundCount.setText(count + "");
                lbFinishCount.setText((double) Math.round(del * 1000 / found) / 10.0 + "%");
            }

            @Override
            public void foundSpace(long space) {
                String size = FileCommonUtil.getSize(space);
                System.out.println("发现" + size + "文件");
                lbFoundSpace.setText(size);
            }

            @Override
            public void delCount(long count) {
                del = count;
                System.out.println("删除" + count + "个文件");
                lbDelCount.setText(count + "");
                lbFinishCount.setText((double) Math.round(del * 1000 / found) / 10.0 + "%");

            }

            @Override
            public void delSpace(long space) {
                String size = FileCommonUtil.getSize(space);
                System.out.println("删除" + size + "文件");
                lbDelSpace.setText(size);
            }

            @Override
            public void finish(String filePath) {
                System.out.println("删除完成：" + filePath);
                lbFinishStatus.setText("删除完成：" + filePath);
                lbFinishCount.setText((double) Math.round(del * 1000 / found) / 10.0 + "%");

            }

            @Override
            public void error(FileManage.DelErrorType delErrorType) {
                System.out.println(delErrorType == FileManage.DelErrorType.NOTHINGNESS ? "文件不存在！" : "其他错误");
                lbFinishStatus.setText(delErrorType == FileManage.DelErrorType.NOTHINGNESS ? "文件不存在！" : "其他错误");
            }
        };
