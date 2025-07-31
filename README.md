import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/tertiary_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/bill_payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/biller_image.dart';
import 'package:hdfc_flutter_widgets/event_card/common/event_execution_pill.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';

/// A reusable and responsive compact event card widget.
/// Use this to show payment/event-related information in a summarized format.
class CompactEventCard extends StatelessWidget {
  /// List of menu options shown in the more options icon.
  final List<String> menuOptions;

  /// Callback when user taps 'View Details' button.
  final VoidCallback onTap;

  /// Callback when a menu option is selected.
  final ValueChanged<String> onSelect;

  /// Path to the event icon (usually an SVG).
  final String prefixIconPath;

  /// Path to the biller logo/icon.
  final String suffixIconPath;

  /// Label text for smart pay status (e.g. "Enabled", "Disabled").
  final String descriptionText;

  /// Icon path for smart pay status.
  final String descriptionIconPath;

  /// Total amount to be paid/shown.
  final double amount;

  /// Status string for the bill (e.g. "Paid", "Overdue").
  final String paymentStatus;

  /// Bill status text background color.
  final Color paymentStatusBackgroundColor;

  /// Bill status text color.
  final Color paymentStatusTextColor;

  /// Scheduled event date string (e.g. "17 Sept").
  final String eventDate;

  /// Scheduled event label (e.g. "SCHEDULED", "PAID").
  final String eventDateLabel;

  /// Event name to display.
  final String eventName;

  /// Background color for event icon.
  final Color backgroundColor;

  /// User account or masked account string.
  final String accountDetails;

  /// Type of bill or service (e.g. "Electricity", "Mobile").
  final String billType;

  /// Text for "View Details" button.
  final String viewDetailsText;

  final String subTitle;

  const CompactEventCard({
    super.key,
    required this.menuOptions,
    required this.onTap,
    required this.onSelect,
    required this.prefixIconPath,
    required this.suffixIconPath,
    required this.descriptionText,
    required this.descriptionIconPath,
    required this.amount,
    required this.paymentStatus,
    required this.paymentStatusBackgroundColor,
    required this.paymentStatusTextColor,
    required this.eventDate,
    required this.eventDateLabel,
    required this.eventName,
    required this.backgroundColor,
    required this.accountDetails,
    required this.billType,
    this.viewDetailsText = "View Details",
    required this.subTitle,
  });

  /// Top container decoration
  BoxDecoration _topContainerDecoration(BuildContext context) => BoxDecoration(
    color: Colors.lightBlue[50],
    border: Border.all(color: Theme.of(context).primaryColor, width: 1.0),
    borderRadius: const BorderRadius.only(
      topLeft: Radius.circular(20),
      topRight: Radius.circular(20),
    ),
  );

  /// Bottom container decoration
  BoxDecoration _bottomContainerDecoration(BuildContext context) => BoxDecoration(
    color: Colors.white,
    borderRadius: const BorderRadius.only(
      bottomLeft: Radius.circular(8),
      bottomRight: Radius.circular(8),
    ),
    border: Border(
      left: BorderSide(color: Theme.of(context).primaryColor, width: 1),
      right: BorderSide(color: Theme.of(context).primaryColor, width: 1),
      bottom: BorderSide(color: Theme.of(context).primaryColor, width: 1),
    ),
  );

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, constraints) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Top section: Event details and smart pay
            Container(
              decoration: _topContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Expanded(
                    child: PrimaryDetail(
                      title: eventName,
                      prefixIconPath: prefixIconPath,
                      prefixIconBackgroundColor: backgroundColor,
                      descriptionIconPath: descriptionIconPath,
                      descriptionText: descriptionText,
                      subtitle: subTitle,
                    ),
                  ),
                  BillerImage(svgPath: suffixIconPath, size: 50),
                ],
              ),
            ),

            // Bottom section: Payment info + actions
            Container(
              decoration: _bottomContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Column(
                children: [
                  // Amount + Bill status + Date pill
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Expanded(
                        child: Row(
                          mainAxisSize: MainAxisSize.min,
                          children: [
                            Flexible(
                              child: Text(
                                '₹ ${amount.toStringAsFixed(2)}',
                                style: const TextStyle(fontSize: 15, fontWeight: FontWeight.bold),
                                overflow: TextOverflow.ellipsis,
                                maxLines: 1,
                              ),
                            ),
                            const SizedBox(width: 10),
                            Flexible(
                              child: BillPaymentStatus(
                                status: paymentStatus,
                                borderTextColor: paymentStatusTextColor,
                                backgroundColor: paymentStatusBackgroundColor,
                              ),
                            ),
                          ],
                        ),
                      ),
                      EventExecutionPill(eventDate: eventDate, eventString: eventDateLabel),
                    ],
                  ),
                  const SizedBox(height: 10),

                  // Bottom actions
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Expanded(
                        child: SecondaryButton(title: viewDetailsText, onTap: onTap),
                      ),
                      const SizedBox(width: 10),
                      TertiaryButton(
                        options: menuOptions,
                        onSelect: onSelect,
                        icon: const Icon(Icons.more_vert),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        );
      },
    );
  }
}
