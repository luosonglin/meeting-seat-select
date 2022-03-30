<template>
	<div class="main-content">
		<div class="main-left-content">
			<div style="height: 6%;">人员名单</div>
			<el-table ref="singleTable" v-if="tableData != null" :data="tableData" highlight-current-row
				@current-change="handleCurrentChange" style="width: 100%">
				<el-table-column type="index" width="40">
				</el-table-column>
				<el-table-column property="name" width="50">
				</el-table-column>
				<el-table-column property="address" show-overflow-tooltip>
				</el-table-column>
			</el-table>
			<div v-else>
				<el-empty description="暂无数据" style="height: 88%;"></el-empty>
				<el-button plain style="height: 6%;"> + 导入 </el-button>
			</div>
		</div>
		<div class="main-right-content">
			<div style="height: 6%;">
				<div>会议室</div>
				<el-button plain style="font-size: 6sp;position: absolute;top: 0;right: 0;" size="mini"
					@click="dialogVisible = true"> 规格 </el-button>

			</div>
			<div style="height: 88%;">
				<!--  -->
				<div class="allseat">
					<div class="leftUp">
						<div class="seatTitle">
							<img src="../assets/img/background.png" />
						</div>
						<div class="seatbody" v-if="seatArray.length > 1">
							<div v-for="row in seatRow" :key="row">
								<div v-for="col in seatCol" :key="col" class="seat"
									:style="{width:seatWidth+'px',height:seatHeight+'px',display:'inline-block'}">
									<div class="inner-Seat"
										:class="(seatArray[row-1][col-1]===1?'selected-seat':'unselected-seat')"
										@click="handleChooseSeat(row-1,col-1)">
									</div>
								</div>
							</div>
						</div>
						<ul class="clearfix">
							<li>
								<span class="unselected-seat"></span>
								可选座位
							</li>
							<li>
								<span class="selected-seat"></span>
								已选座位
							</li>
						</ul>
					</div>
					<div class="leftDown">
						<div class="seatChooseInfor">
							<div></div>
							<p>共有座位{{seatRow * seatCol}}个，当前已选座{{num}}个</p>
						</div>
					</div>
				</div>


			</div>
		</div>
		<el-dialog title="设置会议室规格" :visible.sync="dialogVisible" width="80%">
			<div class="main-popupwindow">
				<div class="left-popupwindow">
					1、会场座位
					<div style="display: flex;flex-direction: row;justify-content: center;margin-top: 20px;">
						<div>排数</div>
						<el-input type="number" placeholder="行" v-model="seatRowInput" style="width: 100px;"
							size="mini">
						</el-input>
					</div>
					<div style="display: flex;flex-direction: row;justify-content: center;margin-top: 20px;">
						<div>座数</div>
						<el-input type="number" placeholder="座" v-model="seatColInput" style="width: 100px;"
							size="mini">
						</el-input>
					</div>
				</div>
				<div class="center-popupwindow">
					2、会议桌选择
					<div style="display: flex;flex-direction: column; margin-top: 20px;align-items: center;">
						<div
							style="display: flex;flex-direction: row;width: 250px;background-color: #D7D7D7;align-items: center;justify-content: center;">
							<el-radio v-model="desk" label="1">矩形桌</el-radio>
							<img src="../../public/seat1.jpg" />
						</div>
						<div
							style="display: flex;flex-direction: row;width: 250px;background-color: #D7D7D7;justify-content: center;align-items: center;margin-top: 20px;">
							<el-radio v-model="desk" label="2">圆桌</el-radio>
							<img src="../../public/seat2.jpg" />
						</div>
						<div
							style="display: flex;flex-direction: row;width: 250px;background-color: #D7D7D7;justify-content: center;align-items: center;margin-top: 20px;">
							<el-radio v-model="desk" label="3">无桌</el-radio>
							<img src="../../public/seat3.jpg" />
						</div>
					</div>
					<div style="margin-top: 40px;margin-left: 150px;">(会议桌默认置于会议室中央)</div>
				</div>
				<div class="right-popupwindow">
					3、入座方式
					<div style="display: flex;flex-direction: column;align-items: flex-start;margin-top: 20px;">
						<el-radio v-model="radio" label="1">从上到下，环形入座，从内环到外环</el-radio>
						<br />
						<el-radio v-model="radio" label="2">从下到上，环形入座，从内环到外环</el-radio>
						<br />
						<el-radio v-model="radio" label="3">从中间开始，左右入座</el-radio>
						<br />
						<el-radio v-model="radio" label="4">从中间开始，右左入座</el-radio>
					</div>
				</div>
			</div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="dialogVisible = false">取 消</el-button>
				<el-button type="primary" @click="confirmMeetingRoom()">确 定</el-button>
			</span>
		</el-dialog>
	</div>

</template>

<script>
	export default {
		name: 'SeatSelect',
		components: {},
		data() {
			return {
				tableData: [{
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}, {
					name: 'XXX',
					address: 'XXX单位-XXX岗位'
				}],
				dialogVisible: false,
				seatRowInput: 0,
				seatColInput: 0,
				seatRow: 10,
				seatCol: 1s0,
				desk: '0',
				radio: '1',
				seatArray: [],
				seatWidth: 50,
				seatHeight: 30,
				num: 0,
				selectTicket: [],
				ok: 0,
				id: null,
				selected: []

			}
		},
		mounted() {
			this.initSeatArray();
		},
		methods: {
			handleCurrentChange(val) {
				console.log(val)
			},
			confirmMeetingRoom() {
				this.dialogVisible = false
				this.seatRow = Number(this.seatRowInput)
				this.seatCol = Number(this.seatColInput)
				console.log('TAG', this.seatRow+' '+this.seatCol)
				this.initSeatArray();
			},
			//初始座位数组
			initSeatArray() {
				if (this.seatRow == 0 || this.seatCol == 0)
					return
				let seatArray = Array(this.seatRow).fill(0).map(() => Array(this.seatCol).fill(0));
				this.seatArray = seatArray
				console.log('seatArray', this.seatArray)
			},

			handleChooseSeat(x, y) {
				this.ok++;
				console.log(this.num);
				let seatValue = this.seatArray[x][y];
				// let newArray = this.seatArray;
				if (seatValue === 1) {	// 1  已选座位
					// newArray[x][y]=0;
					let onum = this.selectTicket.findIndex(item => item.row == x + 1 && item.col == y + 1);
					this.remove(onum);

				} else if (seatValue === 0) {	// 0  可选座位
					this.num++;
					// newArray[x][y]=1;
					this.selectTicket.push({
						row: x + 1,
						col: y + 1,
						id: this.ok
					});

					console.log(this.selectTicket)
				}
				// this.seatArray = newArray.slice(); 
				
				//思考 -1  无座位，桌子/过道
			},
			remove: function(onum) {
				this.selectTicket.splice(onum, 1);
				this.num--;
			},
		},
		watch: {
			selectTicket: function() {
				this.initSeatArray();
				let newArray = this.seatArray;
				this.selectTicket.forEach(item => {
					newArray[item.row - 1][item.col - 1] = 1;
				})
			},
			selected: function() {
				this.initSeatArray();
			}
		},

	}
</script>

<style>
	.main-content {
		width: 99%;
		height: 96%;
		display: flex;
		flex-direction: row;
		text-align: center;
	}

	.main-left-content {
		width: 20%;
		height: 100%;
		margin-right: 1%;
		background-color: skyblue;
		border: 1px solid rgba(216, 215, 215, 1);
		box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
		border-radius: 6px;
		background-color: #fff;
		padding: 0.625rem;
	}

	.main-right-content {
		width: 80%;
		height: 100%;
		background-color: powderblue;
		border: 1px solid rgba(216, 215, 215, 1);
		box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
		border-radius: 6px;
		background-color: #fff;
		padding: 0.625rem;
	}

	.main-popupwindow {
		display: flex;
		justify-content: space-around;
	}

	.left-popupwindow {
		width: 30%;
		border: 1px solid rgba(216, 215, 215, 1);
		border-radius: 6px;
		margin: 10px;
		padding: 10px;
	}

	.center-popupwindow {
		width: 40%;
		border: 1px solid rgba(216, 215, 215, 1);
		border-radius: 6px;
		margin: 10px;
		padding: 10px;
	}

	.right-popupwindow {
		width: 30%;
		border: 1px solid rgba(216, 215, 215, 1);
		border-radius: 6px;
		margin: 10px;
		padding: 10px;
	}

	.unselected-seat {
		background: url('../assets/img/unselected.png') center center no-repeat;
		background-size: auto 88%;
	}

	.selected-seat {
		background: url('../assets/img/selected.png') center center no-repeat;
		background-size: auto 88%;
	}

	.ticket {
		width: 1000px;
		height: 600px;
		margin: 50px auto;
		min-width: 1000px;
		border: 1px solid rgba(207, 203, 203, .5);
		display: flex;
	}

	.left {
		width: 680px;
		box-sizing: border-box;
		padding: 20px;

		display: flex;
	}

	.left .coulmn {
		width: 60px;
		margin-top: 50px;
		list-style-type: none;
	}

	.left .coulmn li {
		width: 16px;
		height: 16px;
		text-align: center;
		border-radius: 50%;
		background-color: #AEAEAE;
		line-height: 16px;
		/* box-sizing: border-box; */
		margin-top: 20px;
	}

	.left .coulmn li:nth-of-type(1) {
		margin-top: 10px;
	}

	.right {
		flex: 1;
	}

	.leftUp {
		height: 460px;
	}

	.seatTitle {
		width: 100%;
		height: 40px;
	}

	.seatbody {
		width: 100%;
		height: 370px;
		/* background-color:aliceblue; */
		overflow-y: scroll;
		text-align: center;
	}

	.seatbody::-webkit-scrollbar {
		display: none;
	}

	.inner-Seat {
		width: 100%;
		height: 100%;
	}

	.leftDown {
		border-top: 1px solid rgba(207, 203, 203, .5);
	}

	.leftDown .seatChooseInfor {
		height: 100px;
		/* background-color:aliceblue; */
	}

	.clearfix {
		height: 28px;
		display: flex;
	}

	.clearfix li {
		vertical-align: middle;
		list-style-type: none;
		flex: 1;
	}

	.clearfix li span {
		vertical-align: -5px;
		display: inline-block;
		width: 26px;
		height: 25px;
	}

	.seatChooseInfor p {
		text-align: center;
		font-size: 12px;
	}

	/* 右边的 */
	.right {
		box-sizing: border-box;
		padding: 20px 0 0 20px;
		background-color: #FFF5F5;
		max-width: 320px;
	}

	.rightUp {
		padding: 0 10px 20px 0;
		height: 115px;
		display: flex;
	}

	.rightUp .oimage {
		width: 80px;
		height: 113px;
	}

	.rightUp .oimage img {
		width: 100%;
		height: 100%;
	}

	.rightUp .msg {
		flex: 1;
		padding: 0 0 0 10px;
		font-size: 14px;
	}

	.rightUp .msg div:nth-of-type(1) {
		font-weight: 700;
		padding: 5px;
	}

	.rightUp .msg div:nth-of-type(n+2) {
		padding: 5px;
		color: #666;
	}

	.rightDown .place,
	.ting,
	.once {
		font-size: 14px;
		color: #9a9a9a;
		height: 35px;
	}

	.rightDown span {
		font-size: 16px;
	}

	.place span,
	.ting span {
		font-weight: bold;
		color: #3e3e3e;
	}

	.once span {
		color: #eb002a;
		font-weight: bold;
	}

	.rightDown .oseat .piao {
		margin-top: 10px;
		display: flex;
		flex-wrap: wrap;
	}

	.rightDown .oseat {
		font-size: 14px;
		color: #9a9a9a;
		min-height: 70px;
	}

	.rightDown .oseat .xiaopiao {
		width: 48px;
		height: 26px;
		color: #eb002a;
		font-size: 12px;
		background-color: #fff;
		margin: 0px 24px 10px 0;
		padding: 0 5px;
		border: 1px solid #eb002a;
		line-height: 26px;
	}

	.jiage {
		height: 70px;
		border-top: 1px solid rgba(207, 203, 203, .5);
		border-bottom: 1px solid rgba(207, 203, 203, .5);
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.jiage .yuanjia,
	.allplace {
		top: 5px;
		font-size: 14px;
		color: #9a9a9a;
		padding: 5px 0;
	}

	.xiadan {
		width: 155px;
		height: 42px;
		font-size: 14px;
		color: #fff;
		background-color: #eb002a;
		margin: 40px 0 0;
		line-height: 42px;
		text-align: center;
	}
</style>
