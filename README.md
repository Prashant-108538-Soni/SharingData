import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/tertiary_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/bill_payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/biller_image.dart';
import 'package:hdfc_flutter_widgets/event_card/common/event_execution_pill.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_pay_status.dart';

class CompactEventCard extends StatelessWidget {
  final List<String> menuOptions;
  final String eventIconPath;
  final String billerImagePath;
  final String smartPayStatus;
  final double amount;
  final String scheduledDate;
  final VoidCallback onTap;
  final ValueChanged<String> onSelect;
  final String smartPayIconPath;

  // Primary details
  final String eventName;
  final Color backgroundColor;
  final String accountDetails;
  final String billType;

  const CompactEventCard({
    Key? key,
    required this.menuOptions,
    required this.onTap,
    required this.onSelect,
    required this.eventIconPath,
    required this.billerImagePath,
    required this.smartPayStatus,
    required this.amount,
    required this.scheduledDate,
    required this.eventName,
    required this.backgroundColor,
    required this.accountDetails,
    required this.billType,
    required this.smartPayIconPath,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Use LayoutBuilder for responsive sizing
    return LayoutBuilder(
      builder: (context, constraints) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            Container(
              decoration: BoxDecoration(
                color: Colors.lightBlue[50],
                border: Border.all(
                  color: Theme.of(context).primaryColor, // Set the border color here
                  width: 1.0, // Set the border width here
                ),
                borderRadius: BorderRadius.only(
                  topLeft: Radius.circular(20),
                  topRight: Radius.circular(20),
                ),
              ),
              child: Padding(
                padding: const EdgeInsets.only(left: 10, right: 10, top: 15),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.start,
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    /// Top Row: Left icon, Title + ID, Right Logo
                    Row(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        // Left: SVG Icon
                        Flexible(
                          child: PrimaryDetail(
                            eventName: eventName,
                            svgPath: eventIconPath,
                            backgroundColor: backgroundColor,
                            accountDetails: accountDetails,
                            billType: billType,
                          ),
                        ),
                        BillerImage(svgPath: billerImagePath, size: 50),
                      ],
                    ),
                    const SizedBox(height: 10),
                    Padding(
                      padding: const EdgeInsets.symmetric(horizontal: 20),
                      child: SmartPayStatus(svgPath: smartPayIconPath, text: smartPayStatus),
                    ),
                    const SizedBox(height: 20),
                  ],
                ),
              ),
            ),
            Container(
              decoration: BoxDecoration(
                color: Colors.white,
                borderRadius: BorderRadius.only(
                  bottomLeft: Radius.circular(8),
                  bottomRight: Radius.circular(8),
                ),
                border: Border(
                  left: BorderSide(color: Theme.of(context).primaryColor, width: 1),
                  right: BorderSide(color: Theme.of(context).primaryColor, width: 1),
                  bottom: BorderSide(color: Theme.of(context).primaryColor, width: 1),
                  // No 'top' BorderSide is specified, so no top border will be rendered.
                ),
              ),
              child: Padding(
                padding: const EdgeInsets.only(left: 10, right: 10, top: 15, bottom: 10),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.start,
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Row(
                      // Align items along the main axis (horizontal)
                      // spaceBetween puts the first item(s) at the start and the last item(s) at the end,
                      // distributing the remaining space between them.
                      mainAxisAlignment: MainAxisAlignment.spaceBetween,
                      children: [
                        // Group the Amount and BillPaymentStatus together on the left
                        Flexible(
                          child: Row(
                            mainAxisSize: MainAxisSize.min,
                            children: [
                              // Amount
                              Flexible(
                                child: Text(
                                  '₹ ${amount.toStringAsFixed(2)}',
                                  style: const TextStyle(fontSize: 15, fontWeight: FontWeight.bold),
                                  overflow: TextOverflow.ellipsis,
                                  maxLines: 2,
                                ),
                              ),
                              const SizedBox(width: 10),
                              Flexible(
                                child: BillPaymentStatus(
                                  status: "Paid",
                                  borderTextColor: Colors.red,
                                  backgroundColor: Colors.red.shade50,
                                ),
                              ),
                            ],
                          ),
                        ),
                        // Scheduled date pill
                        Flexible(
                          child: EventExecutionPill(eventDate: '17 Sept', eventString: 'SCHEDULED'),
                        ),
                      ],
                    ),

                    const SizedBox(height: 10),

                    /// Bottom: View Details + 3-dot icon
                    Row(
                      mainAxisAlignment: MainAxisAlignment.spaceBetween,
                      children: [
                        // View Details Button
                        Expanded(
                          child: SecondaryButton(title: "View Details", onTap: onTap),
                        ),
                        const SizedBox(width: 10),
                        // More Options Icon
                        TertiaryButton(
                          options: menuOptions,
                          onSelect: onSelect,
                          icon: Icon(Icons.more_vert),
                        ),
                      ],
                    ),
                  ],
                ),
              ),
            ),
          ],
        );
      },
    );
  }
}
